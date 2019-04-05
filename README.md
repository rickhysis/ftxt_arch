# GitHub repository:

https://github.com/sergii-savchenko/rkcp_arch

# Installation

To use CLI to render document, please install (depending on your system configuration, you may need to use `sudo    `):

```
npm install -g markdown-cli-renderer
npm install -g babel-runtime
```

## Rendering document

To render current version just type:

`./render.sh`

## Viewing current documents


We recommend using MS VSCode for this:

https://code.visualstudio.com/download

With installed plugins:

* Mermaid preview
* Markdown Preview Mermaid support

After installing those plugins you should see something like this:

![](./assets/vscode.png)


# User Create Document for KYC


```mermaid
sequenceDiagram
    participant User
    participant Proxy
    participant AppLogic
    participant Barong

    User->>Proxy: request POST '{APPLOGIC}/v1/users/profiles'
    Proxy->>AppLogic: redirect POST '{APPLOGIC}/v1/users/profiles'
    AppLogic->>Barong: redirect POST '{BARONG}/api/v1/profiles'

    Barong-->>AppLogic: Respone Created Profiles
    AppLogic-->>User: Respone Created Profiles
    
    User->>Proxy: request POST '{APPLOGIC}/v1/users/documents'
    Proxy->>AppLogic: redirect POST '{APPLOGIC/v1/users/documents'
    Proxy->>Barong: redirect POST '{BARONG}/api/v1/documents'

    Barong-->>AppLogic: Respone Created Document
    AppLogic-->>User: Respone Created Document

```


# Deposit

### first getting deposit address 

```mermaid
sequenceDiagram
    participant User
    participant Proxy
    participant AppLogic
    participant Peatio

    User->>Proxy: request GET '{APPLOGIC}/v1/funds/deposit_address'
    Proxy->>AppLogic: redirect GET '{APPLOGIC}/v1/funds/deposit_address'
    AppLogic->>Peatio: redirect GET '{PEATIO}/api/v2/deposit_address'
    Peatio-->>AppLogic: response deposit address
    AppLogic->>Peatio: request POST '{PEATIO}/api/v2/deposit_address' create deposit address
    
    Peatio-->>AppLogic: Respone Created Deposit Address 
    AppLogic->>Peatio: request GET '{PEATIO}/api/v2/deposit_address'
    Peatio-->>AppLogic: Respone Deposit Address 
    AppLogic-->>User: Respone Deposit Address
    
```

