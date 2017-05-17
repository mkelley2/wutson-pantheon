** Summary **
Subfields is an implementation of core's Field UI that allows you to split a
single field into as many sub-fields as you like. It is a lot Composed Field ,
but each value is stored as a text string so it is searchable and available to
Views.

You can configure each sub-field type as if it were literally a single field.
This module only supports select list and textfield input boxes. But is also
provides a regex validation handler to validate that appropriate data is
provided.

** Features **
Regex validation (preg_match) on input fields.
Prefix/suffix gets tacked onto fields and stored with the single string.
Full Views and Entity Field Query support.

** How does it work? **
Each field stores its value as a serialized array and string in the database.

* Each array element represents the sub-field value. After that the array is
  serialized and stored into the database as a single value.
* The string value concatenates the prefix, value and suffix together, along
  with all other subfield field elements and gets stored as a single value. Now
  its searchable by Views and Entity Field Query.

** Similar Modules **
Composed Field does not store each of the values as a simple string. So it
doesn't support Views and Entity Field Query. That module also doesn't provide a
mechanism for providing a simple regex validation. One has to use evaluated PHP.

** How to use **
Once you enable this module you will have a new Subfields field type available
in the Field UI.

If you wish to override or extend functionality of this module, it's simple.
Code example below.

function example_form_sku_node_form_alter(&$form, &$form_state, $form_id) {
  $lang = $form['sku_number']['#language'];
  // Loop through all the element children that are numeric array elements.
  foreach (array_filter(element_children($form['sku_number'][$lang]), 'is_numeric') as $delta) {
    $subfields = &$form['sku_number'][$lang][$delta]['subfields'];
    $name = 'sku_number[' . $lang . '][' . $delta . ']';
    // Add #states to only display the second textfield if the first
    // has a value of 'R'.
    $subfields[1]['#states'] = array(
      'visible' => array(
        ':input[name="' . $name . '"]' => array('value' => 'R'),
      ),
    );
    $subfields['#element_validate'][] = 'example_form_sku_node_form_sku_number_validate';
  }
}

function example_form_sku_node_form_sku_number_validate($element, &$form_state, $form) {
  // Clear out any values in the second textfield if the first
  // does not have a value of 'R'.
  if ($element[0]['#value'] != 'R') {
    $parents = $element['#parents'];
    $element[1]['#prefix'] = '';
    $element[1]['#value'] = '';
    drupal_array_set_nested_value($form_state['values'], $parents, $element);
  }
  // If it does have 'R', then it is required.
  elseif (strlen($element[1]['#value']) != 2) {
    form_error($element['subfields'][1], t('Value is required.'));
  }
}


** Contact **
Current maintainer:
Lucas Hedding (heddn) - http://drupal.org/user/1463982
