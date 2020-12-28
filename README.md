# HTML

![tests](https://github.com/gouniverse/html/workflows/tests/badge.svg)

Unpretentious short and sweet HTML Builder.

## Benefits

- Valid (X)HTML
- Programatically generate (X)HTML
- Pure GO code
- No need to transfer HTML files
- No need to embed HTML files

## Example

- Section containing div container (Bootstrap) with a message "Hello world"

```go
import hb "github.com/gouniverse/html"
	
// 1. Create a div container with "Hello world" message
div := hb.NewDiv().Attr("class", "container").HTML("Hello world")

// 2. Create a section with padding of 40px containing the container
section := hb.NewSection().Attr("style","padding:40px;").AddChild(div)

// 3. Render to HTML to display
html := section.ToHTML()
```

!!! For more examples look below in the README

## Installation

```ssh
go get -u github.com/gouniverse/html@v1.10.0
```

## Implemented Tag Shortcuts

- <b>NewButton()</b> - shortcut for <button> tag
- <b>NewCode()</b> - shortcut for <code> tag
- <b>NewDiv()</b> - shortcut for <div> tag
- <b>NewForm()</b> - shortcut for <form> tag
- <b>NewHTML(html string)</b> - adds HTML content to tag
- <b>NewHeading1()</b> - shortcut for <h1> tag
- <b>NewHeading2()</b> - shortcut for <h2> tag
- <b>NewHeading3()</b> - shortcut for <h3> tag
- <b>NewHeading4()</b> - shortcut for <h4> tag
- <b>NewHeading5()</b> - shortcut for <h5> tag
- <b>NewHeading6()</b> - shortcut for <h6> tag
- <b>NewHyperlink()</b> - shortcut for <a> tag
- <b>NewImage()</b> - shortcut for <img> tag
- <b>NewInput()</b> - shortcut for <input> tag
- <b>NewLI()</b> - shortcut for <li> tag
- <b>NewLabel()</b> - shortcut for <label> tag
- <b>NewNav()</b> - shortcut for <nav> tag
- <b>NewNavbar()</b> - shortcut for <navbar> tag
- <b>NewOL()</b> - shortcut for <ol> tag
- <b>NewOption()</b> - shortcut for <option> tag
- <b>NewParagraph()</b> - shortcut for <p> tag
- <b>NewPRE()</b> - shortcut for <pre> tag
- <b>NewScript()</b> - shortcut for <script> tag
- <b>NewScriptURL()</b> - shortcut for <script src="{SRC}"> tag
- <b>NewSelect()</b> - shortcut for <select> tag
- <b>NewSpan()</b>
- <b>NewStyle()</b>
- <b>NewStyleURL()</b>
- <b>NewSection()</b>
- <b>NewTag(tagName string)</b> - for custom tags
- <b>NewTable()</b>
- <b>NewTBody()</b>
- <b>NewTD()</b>
- <b>NewTextArea()</b>
- <b>NewTH()</b>
- <b>NewThead()</b>
- <b>NewTR()</b>
- <b>NewUL()</b> - shortcut for <ul> tag
- <b>NewWebpage()</b> - full HTML page withe head, body, meta, styles and scripts

## Tag Methods

- Attr (shortcut for SetAttribute)
- HTML (shortcut for AddHTML)
- AddChild(tag Tag)
- AddChildren(tag []Tag)
- AddHTML(html string)
- GetAttribute(key string)
- SetAttribute(key, value string)
- ToHTML()

## Webpage Methods
- AddChild(child *Tag)
- SetFavicon(favicon string)
- SetTitle(title string)
- AddScripts(scripts []string)
- AddScript(script string)
- AddScriptURLs(scriptURLs []string)
- AddScriptURL(scriptURL string)
- AddStyle(style string)
- AddStyles(styles []string)
- AddStyleURL(styleURL string)
- AddStyleURLs(styleURLs []string)

## Working with Raw Tags

```go
tag := &Tag{
	TagName: "custom-element",
}
tag.toHTML()
```

## Escaping HTML
For safeguarding HTML use the EscapeString method from the standard HTML library

Link with example: https://golang.org/pkg/html/#EscapeString

## Examples

- Bootstrap login form

```go
// Elements for the form
header := hb.NewHeading3().HTML("Please sign in").Attr("style", "margin:0px;")
emailLabel := hb.NewLabel().HTML("E-mail Address")
emailInput := hb.NewInput().Attr("class", "form-control").Attr("name", "email").Attr("placeholder", "Enter e-mail address")
emailFormGroup := hb.NewDiv().Attr("class", "form-group").AddChild(emailLabel).AddChild(emailInput)
passwordLabel := hb.NewLabel().AddChild(hb.NewHTML("Password"))
passwordInput := hb.NewInput().Attr("class", "form-control").Attr("name", "password").Attr("type", "password").Attr("placeholder", "Enter password")
passwordFormGroup := hb.NewDiv().Attr("class", "form-group").AddChild(passwordLabel).AddChild(passwordInput)
buttonLogin := hb.NewButton().Attr("class", "btn btn-lg btn-success btn-block").HTML("Login")
buttonRegister := hb.NewHyperlink().Attr("class", "btn btn-lg btn-info float-left").HTML("Register").Attr("href", "auth/register")
buttonForgotPassword := hb.NewHyperlink().Attr("class", "btn btn-lg btn-warning float-right").HTML("Forgot password?").Attr("href", "auth/password-restore")

// Add elements in a card
cardHeader := hb.NewDiv().Attr("class", "card-header").AddChild(header)
cardBody := hb.NewDiv().Attr("class", "card-body").AddChildren([]*hb.Tag{
	emailFormGroup,
	passwordFormGroup,
	buttonLogin,
})
cardFooter := hb.NewDiv().Attr("class", "card-footer").AddChildren([]*hb.Tag{
	buttonRegister,
	buttonForgotPassword,
})
card := hb.NewDiv().Attr("class", "card card-default").Attr("style", "margin:0 auto;max-width: 360px;")
card.AddChild(cardHeader).AddChild(cardBody).AddChild(cardFooter)

// Convert to HTML to display
html := card.ToHTML()
```

- Webpage with title, favicon, font-awesome icons, jQuery and Bootstrap

```go
// 1. Webpage Title
title := "Title"

// 2. Webpage Favicon
favicon := "data:image/x-icon;base64,AAABAAEAEBAQAAEABAAoAQAAFgAAACgAAAAQAAAAIAAAAAEABAAAAAAAgAAAAAAAAAAAAAAAEAAAAAAAAABNTU0AVKH/AOPj4wDExMQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACIiAREQEREAIiIBERAREQAiIgIiICIiACIiAiIgIiIAMzMDMzAzMwAzMwMzMDMzACIiAiIgIiIAIiICIiAiIgAzMwMzMDMzADMzAzMwMzMAIiICIiAiIgAiIgIiICIiAAAAAAAAAAAAIiICIiAiIgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA"

// 3. Webpage
webpage := NewWebpage().SetTitle(title).SetFavicon(favicon).AddStyleURLs([]string{
		"https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css",
		"https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css",
	}).AddScriptURLs([]string{
		"https://code.jquery.com/jquery-3.2.1.min.js",
		"https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.bundle.min.js",
	}).AddStyle(`html,body{height:100%;font-family: Ubuntu, sans-serif;}`).AddChild(NewDiv().HTML("Hello"))
```

## Changelog
2020.12.28 - Added shortcuts for <code>, <pre> tags
2020.12.26 - Fix for attribute escapes, added tests
