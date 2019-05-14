# Java JSON Schema Generator
Creating JSON Schema (Draft 7) from your Java classes utilising Jackson (inspired by JJSchema).

## Usage
### Dependency (Maven)

```xml
<dependency>
    <groupId>com.github.victools</groupId>
    <artifactId>jsonschema-generator</artifactId>
    <version>1.0.0</version>
</dependency>
```

### Code
#### Complete/Minimal Example
```java
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.github.victools.jsonschema.generator.SchemaGenerator;
import com.github.victools.jsonschema.generator.SchemaGeneratorConfig;
import com.github.victools.jsonschema.generator.SchemaGeneratorConfigBuilder;
```
```java
ObjectMapper objectMapper = new ObjectMapper();
SchemaGeneratorConfigBuilder configBuilder = new SchemaGeneratorConfigBuilder(objectMapper);
SchemaGeneratorConfig config = configBuilder.build();
SchemaGenerator generator = new SchemaGenerator(config);
JsonNode jsonSchema = generator.generateSchema(YourClass.class);

System.out.println(jsonSchema.toString());
```

#### Toggling Standard Options
```java
import com.github.victools.jsonschema.generator.Option;
import com.github.victools.jsonschema.generator.SchemaGeneratorConfigBuilder;
```
```java
SchemaGeneratorConfigBuilder configBuilder = new SchemaGeneratorConfigBuilder(objectMapper)
    .with(Option.DEFINITIONS_FOR_ALL_OBJECTS, Option.NULLABLE_FIELDS_BY_DEFAULT, Option.NULLABLE_METHOD_RETURN_VALUES_BY_DEFAULT) // default: disabled
    .without(Option.ADDITIONAL_FIXED_TYPES); // default enabled
```

#### Adding Separate Modules (e.g. from another library)
```java
import com.github.victools.jsonschema.generator.Module;
import com.github.victools.jsonschema.generator.SchemaGeneratorConfigBuilder;
```
```java
Module separateModule = new YourSeparateModule();
SchemaGeneratorConfigBuilder configBuilder = new SchemaGeneratorConfigBuilder(objectMapper)
    .with(separateModule);
```
