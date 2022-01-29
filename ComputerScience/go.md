Very first go code
 
    package main
    
    import "fmt"
    
    func main() {
        fmt.Println("Hello World")
    }

Variable declarations

    var card string = "Hello World"
    var card = "Hello World"
    card := "Hello World"

- `:=` only works inside functions. `var card` can work outside functions

functions:

    func name() string {
        return "Hello World"
    }
    
Slices

    cards := []string{"1", "2"}
    cards = append(cards, "3")
    
For loops

    for i, card := range cards {
        fmt.Println(i, card)
    }

Define a type

    type deck []string

Map:

    colors := map[string]string{
        "red": "#ff0000",
    }
    var colors map[string]string
    colors := make(map[string]string)
    
    colors["white"] = "#FFFFFF"
    delete(colors, "white")
    
    for key, value := range colors {
    
    }
zero value of a type: false for booleans, and nil for interfaces and reference types

`_` blank identifier