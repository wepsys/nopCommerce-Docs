---
title: Data Validation
uid: en/developer/tutorials/data-validation
author: git.AndreiMaz
contributors: git.exileDev
---

# Validación de datos

La validación de datos es el proceso de asegurar que un programa funcione con datos limpios, correctos y útiles. La mayoría de los desarrolladores de .NET utilizan validadores de anotaciones de datos. Pero nopCommerce usa Fluent Validation. Es una pequeña biblioteca de validación para .NET que utiliza una interfaz fluida y expresiones lambda para crear reglas de validación para sus objetos comerciales. Debe completar dos pasos para agregar una validación a algunos modelos en nopCommerce:

1. Cree una clase derivada de la clase AbstractValidator y coloque allí toda la lógica necesaria. Vea el código fuente a continuación para tener una idea:

    ```csharp
    public class AddressValidator : BaseNopValidator<AddressModel>
    {
        public AddressValidator(ILocalizationService localizationService)
        {
            RuleFor(x => x.FirstName)
            .NotEmpty()
            .WithMessage(localizationService.GetResource("Admin.Address.Fields.FirstName.Required"))
            .When(x => x.FirstNameEnabled && x.FirstNameRequired);
        }
    }
    ```

1. Anote la clase de su modelo con ValidatorAttribute. Consulte el ejemplo siguiente para obtener orientación.

    ```csharp
    [Validator(typeof(AddressValidator))]
    public partial class AddressModel : BaseNopEntityModel
    {
      //...
    }
    ```

   ASP.NET Core ejecutará el validador apropiado cuando se publique un modelo de vista en un controlador.
