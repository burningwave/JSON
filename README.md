# Burningwave JSON

<a href="https://www.burningwave.org">
<img src="https://raw.githubusercontent.com/burningwave/burningwave.github.io/main/logo.png" alt="logo.png" height="180px" align="right"/>
</a>

**Burningwave JSON** is an advanced, free and open source JSON handler for Java.

And now we will see:
* [including Burningwave JSON in your project](#Including-Burningwave-JSON-in-your-project)
* [finding values ​​and paths in a JSON object](#Finding-values-and-paths-in-a-JSON-object)
* [validating values](#Validating-values)
* [**how to ask for assistance**](#Ask-for-assistance)

<br/>

# <a name="Including-Burningwave-JSON-in-your-project"></a>Including Burningwave JSON in your project 
To include Burningwave JSON library in your projects simply use with **Apache Maven**:

```xml
<dependency>
    <groupId>org.burningwave</groupId>
    <artifactId>json</artifactId>
    <version>0.8.0</version>
</dependency>
```

### Requiring the Burningwave JSON module

To use Burningwave JSON as a Java module you need to add the following to your `module-info.java`: 

```java
requires org.burningwave.json;
```

<br/>

# <a name="Finding-values-and-paths-in-a-JSON-object"></a>Finding values ​​and paths in a JSON object
For this purpose is necessary the use of  **ObjectHandler**. Let's assume the following JSON document:

```json
{
    "quiz": {
        "sport": {
            "q1": {
                "question": "Which one is correct team name in NBA?",
                "options": [
                    "New York Bulls",
                    "Los Angeles Kings",
                    "Golden State Warriros",
                    "Huston Rocket"
                ],
                "answer": "Huston Rocket"
            }
        },
        "maths": {
            "q1": {
                "question": "5 + 7 = ?",
                "options": [
                    "10",
                    "11",
                    "12",
                    "13"
                ],
                "answer": "12"
            },
            "q2": {
                "question": "12 - 8 = ?",
                "options": [
                    "1",
                    "2",
                    "3",
                    "4"
                ],
                "answer": "4"
            }
        }
    }
}
```
Now to load values and retrieve paths you can do the following (the full example is available in the [ObjectHandlerTest class](https://github.com/burningwave/json/blob/main/src/test/java/org/burningwave/json/ObjectHandlerTest.java)):

```java
//Loading the JSON object
Root jsonObject = facade.objectMapper().readValue(
    ObjectHandlerTest.class.getClassLoader().getResourceAsStream("quiz.json"),
    Root.class
);
ObjectHandler objectHandler = facade.newObjectHandler(jsonObject);

ObjectHandler.ValueFinder valueFinder = objectHandler.newValueFinder();
Sport sport = valueFinder.findFirstForPathEndsWith("sport");
String option2OfSportQuestion = valueFinder.findFirstForPathEndsWith(Path.of("sport", "q1", "options[1]"));
Q1 questionOne = valueFinder.findForPathEquals(Path.of("quiz", "sport", "q1"));

ObjectHandler.Finder objectHandlerFinder = objectHandler.newFinder();
ObjectHandler sportOH = objectHandlerFinder.findFirstForPathEndsWith("sport");
//Retrieving the path of the sport object ("quiz.sport")
String sportPath = sportOH.getPath();
//Retrieving the value of the sport object
sport = sportOH.getValue();
ObjectHandler option2OfSportQuestionOH = objectHandlerFinder.findFirstForPathEndsWith(Path.of("sport", "q1", "options[1]"));
String option2OfSportQuestionOHPath = option2OfSportQuestionOH.getPath();
option2OfSportQuestion = option2OfSportQuestionOH.getValue();
ObjectHandler questionOneOH = objectHandlerFinder.findForPathEquals(Path.of("quiz", "sport", "q1"));
String questionOnePath = questionOneOH.getPath();
questionOne = questionOneOH.getValue();
```

<br />

# <a name="Validating-values"></a>Validating values
... Documentation in preparation

<br />

# <a name="Ask-for-assistance"></a>Ask for assistance
If this guide can't help you, you can:
* [open a discussion](https://github.com/burningwave/json/discussions) here on GitHub
* [report a bug](https://github.com/burningwave/json/issues) here on GitHub
* ask on [Stack Overflow](https://stackoverflow.com/search?q=burningwave)
