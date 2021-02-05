---
title: Inversion of Control and Dependency Injection
uid: en/developer/tutorials/inversion-of-control
author: git.AndreiMaz
contributors: git.exileDev
---

# Inversión de control e inyección de dependencia

La inversión de control y la inyección de dependencia son dos formas relacionadas de separar las dependencias en sus aplicaciones. [Inversión de control (IoC)](https://en.wikipedia.org/wiki/Inversion_of_control) significa que los objetos no crean otros objetos en los que se basan para hacer su trabajo. En cambio, obtienen los objetos que necesitan de una fuente externa. [Dependency Injection (DI)](http://en.wikipedia.org/wiki/Dependency_injection) significa que esto se realiza sin la intervención del objeto, generalmente mediante un componente de marco que pasa los parámetros del constructor y establece las propiedades. Martin Fowler ha escrito una gran descripción de Inyección de dependencia o Inversión de control. No voy a duplicar su trabajo y puedes encontrar su artículo aquí. nopCommerce usa la biblioteca [Autofac](https://autofac.org/) como su contenedor de IoC. Una vez que se escribe un servicio y una interfaz adecuada, que el servicio implementa, debe registrarlos en cualquier clase que implemente la interfaz IDependencyRegistrar (espacio de nombres Nop.Core.Infrastructure.DependencyManagement). Por ejemplo, todos los servicios principales de nopCommerce están registrados en la clase **DependencyRegistrar** ubicada en la biblioteca Nop.Web.Framework.

```csharp
    public class DependencyRegistrar : IDependencyRegistrar
    {
        public virtual void Register(ContainerBuilder builder, ITypeFinder typeFinder, NopConfig config)
        {
                builder.RegisterType<WebHelper>().As<IWebHelper>().InstancePerLifetimeScope();
            ...
        }
    }
```

Puede crear tantas clases de registradores de dependencias como necesite. Cada clase que implementa la interfaz **IDependencyRegistrar** tiene una propiedad **Order**. Le permite reemplazar las dependencias existentes. Para anular las dependencias de nopCommerce, establezca la propiedad Order en algo mayor que 0. nopCommerce ordena las clases de dependencia y las ejecuta en orden ascendente. Cuanto mayor sea el número, más tarde se registrarán sus objetos.
