---
title: "Instalar Microsoft R Server desde la línea de comandos | Microsoft Docs"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: b9f6ceba4d3609a7e7ff816d31446a77c4fea64c
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="install-microsoft-r-server-from-the-command-line"></a>Instalar Microsoft R Server desde la línea de comandos
    
En este tema se describe cómo usar argumentos de línea de comandos de SQL Server para instalar a Microsoft R Server en SQL Server 2016 o instalar el servidor de aprendizaje de máquina (independiente) en SQL Server 2017. 

> [!NOTE]
También puede instalar a Microsoft R Server mediante un instalador independiente de Windows. Para obtener más información, consulte [instalar R Server 9.0.1 para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows). 

## <a name="prerequisites"></a>Requisitos previos

Este método de instalación requiere que sepa cómo realizar una instalación de línea de comandos de SQL Server y está familiarizado con los argumentos de secuencias de comandos.

- Para efectuar una instalación**desatendida** , debe especificar la ubicación de la utilidad de instalación y usar argumentos para indicar las características que quiere instalar. 
- Para efectuar una instalación **silenciosa** , proporcione los mismos argumentos y agregue el conmutador **/q** . No se proporcionará ningún mensaje y no se requiere ninguna interacción, pero se producirá un error en el programa de instalación si se omite alguno de los argumentos obligatorios.

Para obtener más información, vea [Instalar SQL Server 2016 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).

## <a name="sql-server-2017-microsoft-machine-learning-server-standalone"></a>SQL Server de 2017: Equipo con Microsoft aprendizaje Server (independiente)

Ejecute el comando siguiente desde un símbolo del sistema con privilegios elevados para instalar solo servidor de aprendizaje de Microsoft máquina (independiente) y sus requisitos previos.  El ejemplo muestra los argumentos usados para instalar R.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MR  /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS 
```

Para ver el progreso y los mensajes, quite el argumento _/q_.

- **CARACTERÍSTICAS = SQL_SHARED_MR** obtiene únicamente los componentes de servidor de aprendizaje de máquina. Esto incluye los requisitos previos, que se instalan en modo silencioso, de forma predeterminada.
- **SQL_INST_MR** es necesario para admitir installl para el lenguaje R.
- **SQL_INST_MPY** es necesario para instalar la compatibilidad con Python.
- **IACCEPTROPENLICENSETERMS** indica que ha aceptado los términos de la licencia para usar los componentes de R de código abierto.
- **IACCEPTPYTHONLICENSETERMS** indica han aceptado los términos de licencia para el uso de los componentes de Python.
- **IACCEPTSQLSERVERLICENSETERMS** es obligatorio para ejecutar el Asistente para la instalación.

**Notas**

1. Se requiere, el argumento de características que los términos de licencia de SQL Server.
2. Especifique al menos un idioma, junto con la marca de contrato de licencia.
3. Puede instalar un idioma, o tanto R y Python, pero tiene una licencia independiente para cada uno.

## <a name="sql-server-2016-microsoft-r-server-standalone"></a>SQL Server 2016: Microsoft R Server (independiente)

Ejecute el siguiente comando desde un símbolo del sistema con privilegios elevados para instalar solo Microsoft R Server (independiente) y sus requisitos previos.  El ejemplo muestra los argumentos usados con el programa de instalación de SQL Server 2016.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

## <a name="offline-installation"></a>Instalación sin conexión

Si instala el servidor de aprendizaje de máquina o Microsoft R Server (independiente) en un equipo que no tenga acceso a Internet, debe descargar los componentes de R necesarios de antemano y cópielos en una carpeta local. Para consultar las ubicaciones de descarga, consulte [Instalación de componentes de R sin acceso a Internet](../r/installing-ml-components-without-internet-access.md).

## <a name="what-is-installed"></a>Lo que está instalado

Una vez concluida la instalación, puede revisar el archivo de configuración creado por el programa de instalación de SQL Server, junto con un resumen de las acciones de instalación.

De forma predeterminada, todo el programa de instalación registros y resúmenes para SQL Server y características relacionadas se crean en las siguientes carpetas:

- SQL Server 2016:`C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log`
- 2017 de SQL Server:`C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`

Se crea una subcarpeta independiente para cada característica instalada.

Para configurar la otra instancia de Microsoft R Server con los mismos parámetros, puede reutilizar el archivo de configuración que se crea durante la instalación. Para obtener más información, vea [instalar SQL Server mediante un archivo de configuración](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)


## <a name="customize-your-r-environment"></a>Personalizar el entorno de R

Después de la instalación, puede instalar más paquetes de R. Para obtener más información, consulte [Installing and Managing R Packages](../r/install-additional-r-packages-on-sql-server.md)(Instalar y administrar paquetes de R).

> [!IMPORTANT]
> Si va a ejecutar el código de R en SQL Server, asegúrese de que instale los mismos paquetes en el equipo que desee utilizar para desarrollar la solución y la instancia de SQL Server en la que ejecutar o implementar la solución.

Después de instalar servicios de aprendizaje de máquina para R (In-Database), puede usar al instalador independiente de Windows para actualizar la versión de R que está asociado a una instancia de SQL Server especificada. Para obtener más información, consulte [SqlBindR de uso para actualizar R](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).



