---
title: 'Paso 1: Configurar el entorno de desarrollo de Python pymssql | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9d74e3ce2f7db91aca295dcb7507431a82e49c8c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803865"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>Paso 1: configurar el entorno de desarrollo para el desarrollo de Python pymssql
Deberá configurar el entorno de desarrollo con los requisitos previos para desarrollar una aplicación con el controlador de Python para SQL Server.    
  
Tenga en cuenta que los controladores de SQL Python utilizan el protocolo TDS, que está habilitado de forma predeterminada en SQL Server y Azure SQL Database.  No se requiere ninguna configuración adicional.  
  
## <a name="windows"></a>Windows  
  
1. **Instalar el runtime de Python y el Administrador de paquetes de pip**  
A. Vaya a [python.org](https://www.python.org/downloads/)  
B. Haga clic en el vínculo apropiado de msi de instalador de Windows.   
c. Ejecutar una vez descargado el archivo msi para instalar el runtime de Python  
  
2. **Descargar el módulo pymssql** desde [aquí](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    Asegúrese de que elegir el archivo whl correcto.  Por ejemplo: elija si usa Python 2.7 en un equipo de 64 bits: pymssql‑2.1.1‑cp27‑none‑win_amd64.whl. Una vez descargado el archivo .whl colocarlo en la carpeta C:/Python27.  
      
3. **Abra cmd.exe**  
  
4. **Instalar el módulo pymssql**     
    Por ejemplo, si usa Python 2.7 en un equipo de 64 bits:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Instalar el runtime de Python y el Administrador de paquetes de pip** Python viene preinstalado en la mayoría de las distribuciones de Ubuntu.  Si el equipo no tiene instalado python, puede obtener Descargue el paquete tarball de origen de [python.org](https://www.python.org/downloads/) y compilar localmente, o puede usar el Administrador de paquetes:  
```  
> sudo apt-get install python   
```  
  
2.  **Abrir terminal**  
  
3.  **Instalar las dependencias y módulo pymssql**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **Instalar el runtime de Python y el Administrador de paquetes de pip**  
A. Vaya a [python.org](https://www.python.org/downloads/)  
B. Haga clic en el vínculo apropiado de paquete de instalador de Mac.   
c. Ejecutar una vez descargado el paquete para instalar el runtime de Python  
  
2.  **Abrir terminal**  
  
3. **Instalar a Administrador de paquetes de Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **Instalar el módulo de FreeTDS**  
```  
> brew install FreeTDS  
```  
  
5.  **Instalar el módulo pymssql**  
```  
> sudo -H pip install pymssql  
```
