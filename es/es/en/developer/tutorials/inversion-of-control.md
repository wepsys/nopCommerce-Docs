---
title: Inversion of Control and Dependency Injection
uid: en/developer/tutorials/inversion-of-control
author: git.AndreiMaz
contributors: git.exileDev
---

# Inversión de la inyección de control y dependencia

La inversión de control y la inyección de dependencia son dos formas relacionadas de romper las dependencias en sus aplicaciones. [Inversión de Control (IoC)](https://en.wikipedia.org/wiki/Inversion_of_control) significa que los objetos no crean otros objetos de los que dependen para hacer su trabajo. En su lugar, obtienen los objetos que necesitan de una fuente externa. Inyección de dependencia (DI)](http://en.wikipedia.org/wiki/Dependency_injection) significa que esto se hace sin la intervención del objeto, generalmente por un componente del marco que pasa los parámetros del constructor y establece las propiedades. Martin Fowler ha escrito una gran descripción de la Inyección de Dependencia o Inversión de Control. No voy a duplicar su trabajo, y puedes encontrar su artículo aquí. nopCommerce utiliza la biblioteca [Autofac](https://autofac.org/) como su contenedor de IO. Una vez escrito un servicio y una interfaz apropiada, que el servicio implementa, debe registrarlos en cualquier clase que implemente la interfaz IDependencia-Registro (Nop.Core.Infrastructure.DependencyManagement namespace). Por ejemplo, todos los servicios centrales de nopCommerce se registran en la clase **DependencyRegistrar** situada en la biblioteca Nop.Web.Framework.

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

Puedes crear tantas clases de registro de dependencia como necesites. Cada clase que implementa la interfaz **IDependencyRegistrar** tiene una propiedad **Orden**. Te permite reemplazar las dependencias existentes. Para anular las dependencias de nopCommerce, establece la propiedad Order en algo mayor que 0. nopCommerce ordena las clases de dependencia y las ejecuta en orden ascendente. Cuanto más alto sea el número, más tarde se registrarán los objetos.
