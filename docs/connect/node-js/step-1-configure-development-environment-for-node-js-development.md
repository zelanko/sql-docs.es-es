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
manager: jroth
ms.openlocfilehash: 49522e397789c5193ed8f218a5fdf776ba62f001
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799360"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>Paso 1: configurar el entorno de desarrollo para el desarrollo de Node.js
Deberá configurar el entorno de desarrollo con los requisitos previos para desarrollar una aplicación con el controlador de Node.js para SQL Server.  El método más común es usar node package manager (npm) para instalar el módulo tedioso, pero puede descargar el módulo directamente en una tarea tediosa [Github](https://github.com/pekim/tedious) si lo prefiere.  
  
Tenga en cuenta que el controlador de Node.js usa el protocolo TDS, que está habilitado de forma predeterminada en SQL Server y Azure SQL Database.  No se requiere ninguna configuración adicional.  
  
## <a name="windows"></a>Windows  
  
1. **Instalar a Administrador de paquetes en tiempo de ejecución y npm de Node.js**  
A. Vaya a [Node.js](https://nodejs.org/en/download/)  
B. Haga clic en el vínculo apropiado de msi de instalador de Windows.   
c. Una vez descargado, ejecute el archivo msi para instalar Node.js  
  
2. **Abra cmd.exe**  
  
3. **Cree un directorio de proyecto** y navegar hasta él.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **Cree un proyecto de nodo.**  Para conservar los valores predeterminados durante la creación del proyecto, presione ENTRAR hasta que se cree el proyecto. Al final de este paso, debería ver un archivo package.json en el directorio del proyecto.  
```  
> npm init  
```  
  
5. **Instale el módulo tedioso en el proyecto.**  Se trata de la implementación del protocolo TDS que el controlador se usa para comunicarse con SQL Server.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **Abrir terminal**  
  
2. **Instalar el runtime de Node.js**  
```  
>sudo apt-get install node  
```  
3. **Instale npm (Administrador de paquetes de nodo)**  
```  
> sudo apt-get install npm  
```  
4. **Cree un directorio de proyecto** y navegar hasta él.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **Cree un proyecto de nodo.**  Para conservar los valores predeterminados durante la creación del proyecto, presione ENTRAR hasta que se cree el proyecto. Al final de este paso, debería ver un archivo package.json en el directorio del proyecto.  
```  
> sudo npm init  
```  
  
6. **Instale el módulo tedioso en el proyecto.**  Se trata de la implementación del protocolo TDS que el controlador se usa para comunicarse con SQL Server.  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **Instalar a Administrador de paquetes en tiempo de ejecución y npm de Node.js**  
A. Vaya a [Node.js](https://nodejs.org/en/download/)  
B. Haga clic en el vínculo apropiado de instalador de Mac OS.  
c. Una vez descargado, ejecute dmg para instalar Node.js  
  
2. **Abrir terminal**  
  
3. **Cree un directorio de proyecto** y navegar hasta él.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **Cree un proyecto de nodo.**  Para conservar los valores predeterminados durante la creación del proyecto, presione ENTRAR hasta que se cree el proyecto. Al final de este paso, debería ver un archivo package.json en el directorio del proyecto.  
```  
> npm init  
```  
  
5. **Instale el módulo tedioso en el proyecto.**  Se trata de la implementación del protocolo TDS que el controlador se usa para comunicarse con SQL Server.  
```  
> npm install tedious  
```  
  
