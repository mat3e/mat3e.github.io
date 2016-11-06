## Domain Objec Reactive Forms
Angular 2 gives a great support for creating [Reactive Forms](https://angular.io/docs/ts/latest/cookbook/dynamic-form.html), which are sometimes called also _Dynamic_ or _Model-driven Forms_.

This library is about taking _Reactive Forms_ to the next level by coupling them with _Domain Objects_.

### Want to create a form field for object's property?
:one: Create  `DorfFieldDefinition` which contains info about a label, validators and more (e.g. type of the input field).
```javascript
    get nameDefinition(): DorfInputDefinition {
        return {
            label: "Name",
            validator: Validators.required,
            type: "text"
        };
    }
```


:two: Create _Component_ which extends `AbstractDorfDetailsComponent` and uses a template similar to _details.view.html_ from the library (or even directly _details.view.html_).
```javascript
    @Component({
        templateUrl: "../../dorf/details.view.html"
    })
    export class ExampleComponent extends AbstractDorfDetailsComponent<ExampleModel> implements OnInit
```


:three: Inside your _Component_ override `getDomainObject` method for returning a domain object:
```javascript
    protected getDomainObject(): ExampleModel {
        return this.model;
    }
```
and `getFieldDefinitions` method for returning _propertyName-fieldDefinition_ map for your object:
```javascript
    protected getFieldDefinitions(): DorfPropertiesToDefinitionsMap<ExampleModel> {
        return {
            "name": this.model.nameDefinition
        }
    }
```

:four: Call `super.ngOnInit();` inside your Component's `ngOnInit` method.

:five: You are done! Enjoy your _Reactive Form_.
