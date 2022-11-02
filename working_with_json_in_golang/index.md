# How to working with JSON in GoLang

In this post, we will learn how to parse json data in GoLang. Have fun!

**Working with structed data**

```go
// Import package
import (
	"encoding/json"
)

type Bird struct {
	Species     string
	Description string
}

func main() {
	jsonString := `{	
		"species": "pigeon",
		"description": "likes to perch on rocks likes to perch on rocks likes to perch on rocks"
	}`
	var bird Bird
	err := json.Unmarshal([]byte(jsonString), &bird)
    if err != nill {
        // json string is invalid.
    }
    ...
}
```
<!--more-->
**Custom attributes name**

```go
...
type Bird struct {
  Species string `json:"birdType"`
  Description string `json:"what it does"`
}
func main()
{
    jsonString := `{
      "birdType": "pigeon",
      "what it does": "likes to perch on rocks"
    }`
    var bird Bird
    err := json.Unmarshal([]byte(birdJson), &bird)
    ...
}
```

**Working with JSON arrays data** 

```go
func main() {
    ...
    jsonString := `[
        {
            "species":"pigeon",
            "decription":"likes to perch on rocks"
        },
        {
            "species":"eagle",
            "description":"bird of prey"
        }
    ]`
    var birds []Bird
    err := json.Unmarshal([]byte(jsonString), &birds)
    ...
}
```
**Working with JSON embedded objects**

```go
...
type Dimensions struct {
  Height int
  Width int
}
...
type Bird struct {
  Species string
  Description string
  Dimensions Dimensions
}
func main() {
    ...
    jsonString := `{
      "species": "pigeon",
      "decription": "likes to perch on rocks"
      "dimensions": {
        "height": 24,
        "width": 10
      }
    }`
    var birds Bird
    err := json.Unmarshal([]byte(jsonString), &birds)
    ...
}
```


**Working with primitives**

Please remember that, primitives are valid JSON string too...
```go
func main() {
    ...
    numberJson := "3"
    floatJson := "3.1412"
    stringJson := `"bird"`

    var n int
    var pi float64
    var str string

    err := json.Unmarshal([]byte(numberJson), &n)
    err = json.Unmarshal([]byte(floatJson), &pi)
    err = json.Unmarshal([]byte(stringJson), &str)
    ...
}
```

**Working with unstructed data**
```go
...
func main() {
    jsonString := `{
      "birds": {
        "pigeon":"likes to perch on rocks",
        "eagle":"bird of prey"
      },
      "animals": "none"
    }`
    var result map[string]interface{}
    err := json.Unmarshal([]byte(birdJson), &result)
    ...
    birds := result["birds"].(map[string]interface{})
    ...
}
```


**Encoding JSON data from GO data**

**Struct data to JSON**
```go
...
type Bird struct {
	Species     string `json:"birdType"`
	Description string `json:"what it does"`
}
func main() {
    pigeon := &Bird{
		Species:     "Pigeon",
		Description: "likes to eat seed",
	}
    data, err := json.Marshal(pigeon)
    if err == nil {
        fmt.Println(string(data))
    } else {
        // Encode error
    }
}
```
Ignoring empty field
```go
type Bird struct {
	Species     string `json:"birdType"`
	Description string `json:"what it does,omitempty"`
}
```

<p style="text-align: right">SRC: <a href="https://www.sohamkamani.com/blog/2017/10/18/parsing-json-in-golang/">https://www.sohamkamani.com/blog/2017/10/18/parsing-json-in-golang/</a></p>

