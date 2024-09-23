# AutoMapper in .NET 8.0 (C#)

Using AutoMapper for Object-Object Mapping in C#

https://medium.com/@nwonahr/using-automapper-for-object-object-mapping-in-c-a8b7bec9590b

### Install
```
Install-Package AutoMapper
```

### Setting Up AutoMapper
```
using AutoMapper;

public class Source
{
    public int Id { get; set; }
    public string Name { get; set; }
}

public class Destination
{
    public int Id { get; set; }
    public string FullName { get; set; }
}

public class MappingProfile : Profile
{
    public MappingProfile()
    {
        CreateMap<Source, Destination>()
            .ForMember(dest => dest.FullName, opt => opt.MapFrom(src => src.Name));
    }
}
```


### Using AutoMapper
```
var config = new MapperConfiguration(cfg => cfg.AddProfile<MappingProfile>());
var mapper = config.CreateMapper();

var source = new Source { Id = 1, Name = "John Doe" };
var destination = mapper.Map<Destination>(source);

Console.WriteLine(destination.FullName); // Output: John Doe
```

## Advanced Mapping Scenarios
AutoMapper supports a variety of advanced mapping scenarios:

+ Flattening: Automatically maps nested properties to a flat structure.
+ Collections: AutoMapper can map collections of objects.
+ Custom Value Resolvers: Use custom logic to resolve the value of a destination property.
+ Null Substitution: Provide a default value if the source value is null.

## Common Use Cases
+ Data Transfer Objects (DTOs): AutoMapper is often used to map between domain models and DTOs.
+ View Models: In ASP.NET MVC or Razor Pages, AutoMapper can map domain models to view models.
+ Service Layer: AutoMapper can simplify mapping between the business logic layer and the data access layer.

## Best Practices with AutoMapper
+ Use Profiles: Always use profiles to organize your mappings. This makes your code more modular and maintainable.
+ Keep It Simple: While AutoMapper supports complex mapping scenarios, try to keep your mappings simple. Complex mappings can be difficult to maintain and debug.
+ Test Your Mappings: Just like any other piece of code, you should test your mappings to ensure they work as expected.
