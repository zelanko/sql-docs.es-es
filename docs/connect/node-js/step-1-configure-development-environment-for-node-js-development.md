---
title: 'Paso 1: Configurar el entorno de desarrollo para el desarrollo de Node.js | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bce89cc12c7493522de55adffb69fcbe3307cbdf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003762"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>Paso 1: configurar el entorno de desarrollo para el desarrollo de Node.js
Tendrá que configurar el entorno de desarrollo con los requisitos previos para desarrollar una aplicación con el controlador node. js para SQL Server.  El método más común es usar el administrador de paquetes de node (NPM) para instalar el módulo tedioso, pero puede descargar el módulo tedioso directamente en [GitHub](https://github.com/pekim/tedious) si lo prefiere.  
  
Tenga en cuenta que el controlador node. js usa el protocolo TDS, que está habilitado de forma predeterminada en SQL Server y Azure SQL Database.  No se requiere ninguna configuración adicional.  
  
## <a name="windows"></a>Windows  
  
1. **Instalar el tiempo de ejecución de node. js y el administrador de paquetes NPM**  
A. Vaya a [node. js](https://nodejs.org/en/download/)  
B. Haga clic en el vínculo MSI de Windows Installer adecuado.   
c. Una vez descargado, ejecute el archivo MSI para instalar node. js.  
  
2. **Abra cmd. exe**  
  
3. **Cree un directorio de proyecto** y navegue hasta él.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **Cree un proyecto de nodo.**  Para conservar los valores predeterminados durante la creación del proyecto, presione entrar hasta que se cree el proyecto. Al final de este paso, debería ver un archivo package. JSON en el directorio del proyecto.  
```  
> npm init  
```  
  
5. **Instale el módulo tedioso en el proyecto.**  Se trata de la implementación del protocolo TDS que el controlador utiliza para comunicarse con SQL Server.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **Abrir terminal**  
  
2. **Instalación del tiempo de ejecución de node. js**  
```  
>sudo apt-get install node  
```  
3. **Instalación de NPM (Administrador de paquetes de node)**  
```  
> sudo apt-get install npm  
```  
4. **Cree un directorio de proyecto** y navegue hasta él.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **Cree un proyecto de nodo.**  Para conservar los valores predeterminados durante la creación del proyecto, presione entrar hasta que se cree el proyecto. Al final de este paso, debería ver un archivo package. JSON en el directorio del proyecto.  
```  
> sudo npm init  
```  
  
6. **Instale el módulo tedioso en el proyecto.**  Se trata de la implementación del protocolo TDS que el controlador utiliza para comunicarse con SQL Server.  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **Instalar el tiempo de ejecución de node. js y el administrador de paquetes NPM**  
A. Vaya a [node. js](https://nodejs.org/en/download/)  
B. Haga clic en el vínculo del instalador de Mac OS adecuado.  
c. Una vez descargado, ejecute el DMG para instalar node. js.  
  
2. **Abrir terminal**  
  
3. **Cree un directorio de proyecto** y navegue hasta él.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **Cree un proyecto de nodo.**  Para conservar los valores predeterminados durante la creación del proyecto, presione entrar hasta que se cree el proyecto. Al final de este paso, debería ver un archivo package. JSON en el directorio del proyecto.  
```  
> npm init  
```  
  
5. **Instale el módulo tedioso en el proyecto.**  Se trata de la implementación del protocolo TDS que el controlador utiliza para comunicarse con SQL Server.  
```  
> npm install tedious  
```  
  
