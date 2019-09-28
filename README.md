## Objectives:
* ASP.NET Core 3 OpenFaaS template for OpenFaaS: https://github.com/openfaas/faas
* Ability to edit and debug from VS Code and Visual Studio
* Leverage of-watchdog

## Project based on
* OpenFaaS watchdog-of templates: https://github.com/openfaas-incubator/of-watchdog
* C# Kestrel template: https://github.com/burtonr/csharp-kestrel-template

## Getting Started
* Create a new ASP.NET Core Function
```
$ faas-cli template pull https://github.com/michaelkacher/openfaas-templates
$ faas-cli new --lang aspnetcore3 my-func
```
* Edit the function
* To run locally
```
$ faas-cli up --skip-push -f my-func.yml
```
* Test it from the UI or CLI
```
$ echo 'hi' | faas-cli invoke my-func
```