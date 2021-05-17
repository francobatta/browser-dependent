# Browser dependent examples
| Browser | fieldset_disabled |
| --- | --- |
| Chrome | Even though the fieldset is disabled, it will will bubble up events to the form |
| Firefox | Events won't 'get past' the fieldset |
| ??? | ??? |
### Fieldset disable behavior
#### How to reproduce
Download [fieldset-disabled.html](fieldset-disabled.html) and open with a browser of your choice. Click the elements and see if an `alert()` is emitted or nothing happens
#### Difference explained
Quoting the HTML spec: *"[in a fieldset], **disabled** causes all the form control descendants of the fieldset element, excluding those that are descendants of the fieldset element's first legend element child, if any, to be disabled"*

**Q: What does it mean for a form control to be disabled?**

A: *A form control that is disabled must prevent any click events that are queued on the user interaction task source from being dispatched on the element*

**Q: And what exactly are form control elements?**

A: according, to MDN web docs, [there are many native form controls](https://developer.mozilla.org/en-US/docs/Learn/Forms/Basic_native_form_controls) plus [some others](https://developer.mozilla.org/en-US/docs/Learn/Forms/Other_form_controls), but an anchor `a` isn't one. A `label`, on the other hand, is a form control

#### Conclusion
It seems some browsers stop propagation of all mouse events from firing, while others only block some elements' events. IMO the latter is correct, because if an element is not a form control, then its events should bubble up to parent as usual
