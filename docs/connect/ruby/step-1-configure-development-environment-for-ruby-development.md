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
manager: craigg
ms.openlocfilehash: a298a7c7f65a198e5bfb0922f2b061fd44079739
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51604705"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>Paso 1: Configurar el entorno de desarrollo para el desarrollo Ruby
Deberá configurar el entorno de desarrollo con los requisitos previos para desarrollar una aplicación con el controlador de Ruby para SQL Server.    
  
Tenga en cuenta que el controlador de Ruby utiliza el protocolo TDS, que está habilitado de forma predeterminada en SQL Server y Azure SQL Database.  No se requiere ninguna configuración adicional.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Descargue el instalador de Ruby**  
Si el equipo no tiene Ruby instálelo. Para los nuevos usuarios de ruby, se recomienda que usar a los instaladores de Ruby 2.2. x. Proporcionan un lenguaje estable y una amplia lista de paquetes (gemas) que son compatibles y actualizados. Vaya el [página de descarga de Ruby](https://rubyinstaller.org/downloads/) y descargue el instalador adecuado 2.1. x. Por ejemplo, si se encuentra en un equipo de 64 bits, descargue el instalador de Ruby 2.1.6 (x 64).   
  
2.  **Instalación de Ruby**  
Una vez descargado el instalador, haga lo siguiente:  
A. Haga doble clic en el archivo para iniciar al instalador.  
B. Seleccione su idioma y acepte los términos.  
c.  En la pantalla de configuración de la instalación, seleccione las casillas de verificación junto a los dos archivos ejecutables de Ruby de agregar a los archivos. RB y .rbw ruta de acceso y asociar con esta instalación de Ruby.  
  
3.  **Descargar DevKit Ruby**  
Descargue el DevKit en la página RubyInstaller  
  
4.  **Instale Ruby DevKit**  
Una vez finalizada la descarga, haga lo siguiente:  
A. Haga doble clic en el archivo. Se le pedirá donde extraer los archivos.  
B. Haga clic en el botón "..." y seleccione "C:\DevKit". Probablemente, deberá crear esta carpeta en primer lugar, haga clic en "Crear nueva carpeta".  
c. Haga clic en "Aceptar" y, a continuación, "extraer", para extraer los archivos.  
  
5. **Abra cmd.exe**  
  
6. **Inicialice Ruby DevKit**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **Instalar la gema TinyTDS**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Abrir terminal**  
  
2. **Instalar Administrador de versión de Ruby (rvm) y los requisitos previos**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Use rvm para instalar Ruby**  
Por ejemplo, instale la versión 2.3.0 de Ruby:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Asegúrese de que el resultado del último comando indica que está ejecutando la versión 2.3.0.  
  
4.  **Instalación de FreeTDS**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **Instalar TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
Tenga en cuenta que Mac OS X ya tiene Ruby previamente instalado, ya que el sistema operativo tiene una dependencia.    
  
1.  **Abrir terminal**  
  
2. **Instalar a Administrador de paquetes de Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **Instalación de FreeTDS**  
```  
> brew install FreeTDS  
```  
  
4.  **Instalar la gema TinyTDS**  
```  
> gem install tiny_tds  
```
