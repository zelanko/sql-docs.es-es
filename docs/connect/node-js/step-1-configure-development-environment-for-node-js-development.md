---
title: 'Paso 1: Configurar el entorno de desarrollo para el desarrollo de Node.js | Documentos de Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: node-js
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7d723913fbc63e65a28031421da004e942f49f6e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>Paso 1: Configurar el entorno de desarrollo para la implementación de Node.js
Debe configurar el entorno de desarrollo con los requisitos previos para desarrollar una aplicación con el controlador Node.js para SQL Server.  El método más común consiste en usar el Administrador de paquetes de nodo (npm) para instalar el módulo tedioso, pero puede descargar el módulo tedioso directamente en [Github](https://github.com/pekim/tedious) si lo prefiere.  
  
Tenga en cuenta que el controlador Node.js utiliza el protocolo TDS, que está habilitado de forma predeterminada en SQL Server y base de datos de SQL Azure.  No se requiere ninguna configuración adicional.  
  
## <a name="windows"></a>Windows  
  
1. **Instalar el Administrador de paquetes npm y tiempo de ejecución de Node.js**  
a. Vaya a [Node.js](https://nodejs.org/en/download/)  
b. Haga clic en el vínculo apropiado de msi de instalador de Windows.   
c. Una vez descargado, ejecute el archivo msi para instalar Node.js  
  
2. **Abra cmd.exe**  
  
3. **Crear un directorio de proyecto** y navegar hasta él.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **Cree un proyecto de nodo.**  Para conservar los valores predeterminados durante la creación del proyecto, presione ENTRAR hasta que se cree el proyecto. Al final de este paso, debería ver un archivo package.json en el directorio del proyecto.  
```  
> npm init  
```  
  
5. **Instalar el módulo tedioso en su proyecto.**  Se trata de la implementación del protocolo TDS que el controlador utiliza para comunicarse con SQL Server.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **Abra terminal**  
  
2. **Instalar Node.js en tiempo de ejecución**  
```  
>sudo apt-get install node  
```  
3. **Instale npm (Administrador de paquetes de nodo)**  
```  
> sudo apt-get install npm  
```  
4. **Crear un directorio de proyecto** y navegar hasta él.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **Cree un proyecto de nodo.**  Para conservar los valores predeterminados durante la creación del proyecto, presione ENTRAR hasta que se cree el proyecto. Al final de este paso, debería ver un archivo package.json en el directorio del proyecto.  
```  
> sudo npm init  
```  
  
6. **Instalar el módulo tedioso en su proyecto.**  Se trata de la implementación del protocolo TDS que el controlador utiliza para comunicarse con SQL Server.  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **Instalar el Administrador de paquetes npm y tiempo de ejecución de Node.js**  
a. Vaya a [Node.js](https://nodejs.org/en/download/)  
b. Haga clic en el vínculo apropiado de instalador de Mac OS.  
c. Una vez descargado, ejecute el dmg para instalar Node.js  
  
2. **Abra terminal**  
  
3. **Crear un directorio de proyecto** y navegar hasta él.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **Cree un proyecto de nodo.**  Para conservar los valores predeterminados durante la creación del proyecto, presione ENTRAR hasta que se cree el proyecto. Al final de este paso, debería ver un archivo package.json en el directorio del proyecto.  
```  
> npm init  
```  
  
5. **Instalar el módulo tedioso en su proyecto.**  Se trata de la implementación del protocolo TDS que el controlador utiliza para comunicarse con SQL Server.  
```  
> npm install tedious  
```  
  
