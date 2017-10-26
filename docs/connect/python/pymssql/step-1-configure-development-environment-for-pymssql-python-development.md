---
title: 'Paso 1: Configurar el entorno de desarrollo de Python pymssql | Documentos de Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0a1932b41ada3469deed6d36a3c68c3827687cc5
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>Paso 1: Configurar el entorno de desarrollo para pymssql desarrollo Python
Debe configurar el entorno de desarrollo con los requisitos previos para desarrollar una aplicación con el controlador Python para SQL Server.    
  
Tenga en cuenta que los controladores de SQL de Python utilizan el protocolo TDS, que está habilitado de forma predeterminada en SQL Server y base de datos de SQL Azure.  No se requiere ninguna configuración adicional.  
  
## <a name="windows"></a>Windows  
  
1. **Instalar en tiempo de ejecución de Python y pip Administrador de paquetes**  
a. Vaya a [python.org](https://www.python.org/downloads/)  
b. Haga clic en el vínculo apropiado de msi de instalador de Windows.   
c. Ejecutar una vez descargado el archivo msi para instalar en tiempo de ejecución de Python  
  
2. **Descargar el módulo de pymssql** de [aquí](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    Asegúrese de que elige el archivo whl correcto.  Por ejemplo: elija si usas Python 2.7 en un equipo de 64 bits: pymssql‑2.1.1‑cp27‑none‑win_amd64.whl. Una vez que descargue el archivo .whl para colocarlo en la la carpeta C:/Python27.  
      
3. **Abra cmd.exe**  
  
4. **Instalar el módulo de pymssql**     
    Por ejemplo, si usas Python 2.7 en un equipo de 64 bits:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Instalar en tiempo de ejecución de Python y Administrador de paquetes de pip** Python viene preinstalado en la mayoría de las distribuciones de Ubuntu.  Si su equipo no tiene instalado de python, puede obtener cualquier descarga el contenedor de origen tar de [python.org](https://www.python.org/downloads/) compilar localmente, o puede usar el Administrador de paquetes:  
```  
> sudo apt-get install python   
```  
  
2.  **Abra terminal**  
  
3.  **Install pymssql module y dependencias**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **Instalar en tiempo de ejecución de Python y pip Administrador de paquetes**  
a. Vaya a [python.org](https://www.python.org/downloads/)  
b. Haga clic en el vínculo apropiado de pkg de instalador de Mac.   
c. Ejecutar una vez descargado el paquete para instalar en tiempo de ejecución de Python  
  
2.  **Abra terminal**  
  
3. **Instalar el Administrador de paquetes de Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **Instalar el módulo de uso**  
```  
> brew install FreeTDS  
```  
  
5.  **Instalar el módulo de pymssql**  
```  
> sudo -H pip install pymssql  
```

