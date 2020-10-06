---
title: 'Paso 1: Configuración del entorno de desarrollo para Ruby'
description: El paso 1 de esta guía de introducción implica la instalación de Ruby y un controlador ODBC para SQL Server en el entorno de desarrollo.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a6412015000a5f9dda09ea5d489c8080fd2e1c09
ms.sourcegitcommit: 2600a414c321cfd6dc6daf5b9bcbc9a99c049dc4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603368"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>Paso 1: Configuración del entorno de desarrollo para el desarrollo Ruby
Tendrá que configurar el entorno de desarrollo con los requisitos previos para desarrollar una aplicación con el controlador de Ruby para SQL Server.    
  
El controlador de Ruby usa el protocolo TDS, que está habilitado de forma predeterminada en SQL Server y Azure SQL Database.  No se requiere ninguna configuración adicional.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Descarga del instalador de Ruby**  
Si el equipo no tiene Ruby, instálelo. En el caso de los nuevos usuarios de Ruby, se recomienda usar los instaladores de Ruby 2.2. X, que proporcionan un lenguaje estable y una amplia lista de paquetes (archivos gem) compatibles y actualizados. Vaya a la [página de descarga de Ruby](https://rubyinstaller.org/downloads/) y descargue el instalador 2.1.x adecuado. Por ejemplo, si trabaja en un equipo de 64 bits, descargue el instalador de Ruby 2.1.6 (x64).   
  
2.  **Instale Ruby**.  
Una vez descargado el instalador:  
a. Haga doble clic en el archivo para iniciar el instalador.  
b. Seleccione su idioma y acepte los términos.  
c.  En la pantalla Configuración de instalación, seleccione las casillas situadas junto a la opción para agregar archivos ejecutables de Ruby a la RUTA DE ACCESO y asocie los archivos `.rb` y `.rbw` con esta instalación de Ruby.  
  
3.  **Descarga de Ruby DevKit**  
Descargue DevKit desde la página de RubyInstaller.  
  
4.  **Instalación de Ruby DevKit**.  
Una vez finalizada la descarga:  
a. Haga doble clic en el archivo. Se le preguntará dónde extraer los archivos.  
b. Haga clic en el botón "..." y seleccione "C:\DevKit". Probablemente tendrá que crear primero esta carpeta haciendo clic en "Crear nueva carpeta".  
c. Haga clic en "Aceptar" y, a continuación, en "Extraer" para extraer los archivos.  
  
5. **Abra cmd.exe**.  
  
6. **Inicialice Ruby DevKit**.  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **Instale la gema TinyTDS**.  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Abra el terminal**.  
  
2. **Instale el administrador de versiones de Ruby (`rvm`) y los requisitos previos**.  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Use `rvm` para instalar Ruby**.  
Por ejemplo, instale la versión 2.3.0 de Ruby:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Asegúrese de que la salida del último comando indica que está ejecutando la versión 2.3.0.  
  
4.  **Instale FreeTDS**.  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **Instale TinyTDS**.  
```  
> gem install tiny_tds  
```  
  
## <a name="macos"></a>macOS  
  
Nota: macOS ya tiene Ruby preinstalado, ya que el sistema operativo tiene una dependencia.
  
1.  **Abra el terminal**.  
  
2. **Instale el administrador de paquetes de Homebrew**.  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **Instale FreeTDS**.  
```  
> brew install FreeTDS  
```  
  
4.  **Instale la gema TinyTDS**.  
```  
> gem install tiny_tds  
```
