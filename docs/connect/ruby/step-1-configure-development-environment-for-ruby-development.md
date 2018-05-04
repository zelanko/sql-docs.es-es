---
title: 'Paso 1: Configurar el entorno de desarrollo para el desarrollo Ruby | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ruby
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c7052fce85e035a0c4bff543ccbf994d7dd5f44d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>Paso 1: Configurar el entorno de desarrollo para el desarrollo Ruby
Debe configurar el entorno de desarrollo con los requisitos previos para desarrollar una aplicación con el controlador Ruby para SQL Server.    
  
Tenga en cuenta que el controlador de Ruby utiliza el protocolo TDS, que está habilitado de forma predeterminada en SQL Server y base de datos de SQL Azure.  No se requiere ninguna configuración adicional.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Descargue el instalador de Ruby**  
Si su equipo no tiene Ruby debe instalarlo. Para los nuevos usuarios ruby, se recomienda que utilizar a instaladores Ruby 2.2. x. Proporcionan un lenguaje estable y una lista completa de paquetes (gems) que son compatibles y actualizado. Vaya el [página de descarga Ruby](http://rubyinstaller.org/downloads/) y descargar el instalador 2.1 adecuado. Por ejemplo, si se encuentra en un equipo de 64 bits, descargue el instalador de Ruby 2.1.6 (x 64).   
  
2.  **Instalar Ruby**  
Una vez descargado el programa de instalación, haga lo siguiente:  
A. Haga doble clic en el archivo para iniciar el programa de instalación.  
B. Seleccione su idioma y acepte los términos.  
c.  En la pantalla de configuración de la instalación, active las casillas de verificación junto a los ejecutables de Ruby agregar a los archivos de RB y .rbw ruta de acceso y asociar con esta instalación Ruby.  
  
3.  **Descargar DevKit Ruby**  
Descargar DevKit desde la página de RubyInstaller  
  
4.  **Instalar DevKit Ruby**  
Una vez finalizada la descarga, haga lo siguiente:  
A. Haga doble clic en el archivo. Se le pedirá donde extraer los archivos.  
B. Haga clic en el botón "..." y seleccione "C:\DevKit". Probablemente, necesitará crear primero esta carpeta, haga clic en "Crear nueva carpeta".  
c. Haga clic en "Aceptar" y, a continuación, "extraer", para extraer los archivos.  
  
5. **Abra cmd.exe**  
  
6. **Inicializar Ruby DevKit**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **Instalar TinyTDS indicador**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Abra terminal**  
  
2. **Instalar Administrador de versiones de Ruby (rvm) y los requisitos previos**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Utilice rvm para instalar Ruby**  
Por ejemplo, instale la versión 2.3.0 de Ruby:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Asegúrese de que el resultado del último comando indica que está ejecutando la versión 2.3.0.  
  
4.  **Instalar uso**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **Instalar TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
Tenga en cuenta que Mac OS X ya tiene Ruby preinstalado, ya que el sistema operativo tiene una dependencia.    
  
1.  **Abra terminal**  
  
2. **Instalar el Administrador de paquetes de Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **Instalar uso**  
```  
> brew install FreeTDS  
```  
  
4.  **Instalar TinyTDS indicador**  
```  
> gem install tiny_tds  
```
