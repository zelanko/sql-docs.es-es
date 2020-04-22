---
title: 'Paso 1: Configuración del entorno de desarrollo para Node.js'
description: Tendrá que configurar el entorno de desarrollo con los requisitos previos para desarrollar una aplicación mediante el controlador de Node.js para SQL Server.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 38337772d9ec9db2503637122d0d1b616dc6ef5f
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528139"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>Paso 1:  Configuración del entorno de desarrollo para el desarrollo de Node.js
Tendrá que configurar el entorno de desarrollo con los requisitos previos para desarrollar una aplicación mediante el controlador de Node.js para SQL Server.  El método más común es usar el administrador de paquetes de Node (npm) para instalar el módulo tedioso, pero puede descargarlo directamente en [GitHub](https://github.com/pekim/tedious) si lo prefiere.  
  
El controlador de Node.js usa el protocolo TDS, que está habilitado de forma predeterminada en SQL Server y Azure SQL Database.  No se requiere ninguna configuración adicional.  
  
## <a name="windows"></a>Windows  
  
1. **Instale el entorno de ejecución de Node.js y el administrador de paquetes npm.**  
a. Vaya a [Node.js](https://nodejs.org/en/download/).  
b. Haga clic en el vínculo del archivo MSI adecuado de Windows Installer.   
c. Una vez descargado, ejecútelo para instalar Node.js.  
  
2. **Abrir cmd.exe**  
  
3. **Cree un directorio de proyecto** y vaya a él.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **Cree un proyecto de Node.**  Para conservar los valores predeterminados durante la creación del proyecto, presione Entrar hasta que se cree el proyecto. Al final de este paso, verá un archivo package.json en el directorio del proyecto.  
```  
> npm init  
```  
  
5. **Instale el módulo tedioso en el proyecto.**  La implementación del protocolo TDS, que el controlador usa para comunicarse con SQL Server, es tediosa.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **Abra el terminal**.  
  
2. **Instale el entorno de ejecución de Node.js.**  
```  
>sudo apt-get install node  
```  
3. **Instale npm (administrador de paquetes de Node).**  
```  
> sudo apt-get install npm  
```  
4. **Cree un directorio de proyecto** y vaya a él.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **Cree un proyecto de Node.**  Para conservar los valores predeterminados durante la creación del proyecto, presione Entrar hasta que se cree el proyecto. Al final de este paso, verá un archivo package.json en el directorio del proyecto.  
```  
> sudo npm init  
```  
  
6. **Instale el módulo tedioso en el proyecto.**  La implementación del protocolo TDS, que el controlador usa para comunicarse con SQL Server, es tediosa.  
```  
> sudo npm install tedious  
```  
  
## <a name="macos"></a>macOS  
  
1. **Instale el entorno de ejecución de Node.js y el administrador de paquetes npm.**  
a. Vaya a [Node.js](https://nodejs.org/en/download/).  
b. Haga clic en el vínculo del instalador de macOS adecuado.  
c. Una vez descargado, ejecute el archivo "dmg" para instalar Node.js.  
  
2. **Abra el terminal**.  
  
3. **Cree un directorio de proyecto** y vaya a él.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **Cree un proyecto de Node.**  Para conservar los valores predeterminados durante la creación del proyecto, presione Entrar hasta que se cree el proyecto. Al final de este paso, verá un archivo package.json en el directorio del proyecto.  
```  
> npm init  
```  
  
5. **Instale el módulo tedioso en el proyecto.**  Se trata de la implementación del protocolo TDS que el controlador usa para comunicarse con SQL Server.  
```  
> npm install tedious  
```  
