---
title: 'Paso 1: Configurar el entorno de desarrollo para el desarrollo Ruby | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 38af92d3cb0354bc4b75131a349f6a1c26e90490
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992463"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>Paso 1: Configurar el entorno de desarrollo para el desarrollo Ruby
Tendrá que configurar el entorno de desarrollo con los requisitos previos para desarrollar una aplicación con el controlador de Ruby para SQL Server.    
  
Tenga en cuenta que el controlador de Ruby usa el protocolo TDS, que está habilitado de forma predeterminada en SQL Server y Azure SQL Database.  No se requiere ninguna configuración adicional.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Descargar el instalador de Ruby**  
Si el equipo no tiene Ruby, instálelo. En el caso de los nuevos usuarios de Ruby, se recomienda usar los instaladores de Ruby 2.2. X. Proporcionan un lenguaje estable y una amplia lista de paquetes (gemas) que son compatibles y actualizados. Vaya a la [Página de descarga de Ruby](https://rubyinstaller.org/downloads/) y descargue el instalador de 2.1. x adecuado. Por ejemplo, si está en un equipo de 64 bits, descargue el instalador de Ruby 2.1.6 (x64).   
  
2.  **Instalación de Ruby**  
Una vez descargado el instalador, haga lo siguiente:  
A. Haga doble clic en el archivo para iniciar el instalador.  
B. Seleccione su idioma y acepte los términos.  
c.  En la pantalla instalar configuración, active las casillas situadas junto a la opción Agregar archivos ejecutables de Ruby a la ruta de acceso y asocie los archivos. RB y. RBW con esta instalación de Ruby.  
  
3.  **Descargar Ruby DevKit**  
Descarga de DevKit desde la página de RubyInstaller  
  
4.  **Instalación de DevKit de Ruby**  
Una vez finalizada la descarga, haga lo siguiente:  
A. Haga doble clic en el archivo. Se le preguntará dónde extraer los archivos.  
B. Haga clic en "..." y seleccione "C:\DevKit". Probablemente tendrá que crear primero esta carpeta haciendo clic en "crear nueva carpeta".  
c. Haga clic en "Aceptar" y, a continuación, en "extraer" para extraer los archivos.  
  
5. **Abra cmd. exe**  
  
6. **Inicializar Ruby DevKit**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **Instalación de la gema de función tinytds**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Abrir terminal**  
  
2. **Instalar el administrador de versiones de Ruby (RVM) y los requisitos previos**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Uso de RVM para instalar Ruby**  
Por ejemplo, instale la versión 2.3.0 de Ruby:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Asegúrese de que la salida del último comando indica que está ejecutando la versión 2.3.0.  
  
4.  **Instalación de FreeTDS**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **Instalación de función tinytds**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
Tenga en cuenta que Mac OS X ya tiene Ruby preinstalado, ya que el sistema operativo tiene una dependencia.    
  
1.  **Abrir terminal**  
  
2. **Instalación del administrador de paquetes de homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **Instalación de FreeTDS**  
```  
> brew install FreeTDS  
```  
  
4.  **Instalación de la gema de función tinytds**  
```  
> gem install tiny_tds  
```
