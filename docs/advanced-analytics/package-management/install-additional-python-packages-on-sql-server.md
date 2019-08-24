---
title: Instalación de paquetes de Python con PIP
description: Obtenga información sobre cómo usar Python PIP para instalar nuevos paquetes de Python en una instancia de SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 50463f27f37f9da410d1598002989f7cea6d8158
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000772"
---
# <a name="install-python-packages-with-sqlmlutils"></a>Instalación de paquetes de Python con sqlmlutils

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describe cómo usar las funciones del paquete [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) para instalar nuevos paquetes de Python en una instancia de SQL Server Machine Learning Services. Los paquetes que instale se pueden usar en los scripts de Python que se ejecutan en la base de datos mediante la instrucción T-SQL [SP-Execute-external-script-Transact-SQL](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) .

Para obtener más información sobre la ubicación del paquete y las rutas de instalación, vea [obtener información de paquetes de Python](../package-management/python-package-information.md).

> [!NOTE]
> No se recomienda `pip install` el comando estándar de Python para agregar paquetes de Python en SQL Server. En su lugar, use **sqlmlutils** como se describe en este artículo.

## <a name="prerequisites"></a>Requisitos previos

+ Debe tener [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) instalado con la opción de idioma de Python.

+ Instale [Python](https://www.python.org/) en el equipo cliente que usa para conectarse a SQL Server. También puede querer un entorno de desarrollo de Python como [Visual Studio Code](https://code.visualstudio.com/download) con la [extensión de Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python). 

+ Instale [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS) en el equipo cliente que usa para conectarse a SQL Server. Puede usar otras herramientas de consulta o administración de bases de datos, pero en este artículo se da por supuesto Azure Data Studio o SSMS.

### <a name="other-considerations"></a>Otras consideraciones

+ Los paquetes deben ser compatibles con Python 3,5 y ejecutarse en Windows.

+ La biblioteca de paquetes de Python se encuentra en la carpeta archivos de programa de la instancia de SQL Server y, de forma predeterminada, la instalación en esta carpeta requiere permisos de administrador. Para obtener más información, vea ubicación de la [biblioteca de paquetes](../package-management/python-package-information.md#default-python-library-location).

+ La instalación del paquete es por instancia. Si tiene varias instancias de Machine Learning Services, debe agregar el paquete a cada uno de ellos.

+ Antes de agregar un paquete, tenga en cuenta si el paquete es una buena opción para el entorno de SQL Server.

  + Se recomienda usar Python en la base de datos para las tareas que se benefician de la estrecha integración con el motor de base de datos, como machine learning, en lugar de tareas que simplemente consultan la base de datos.

  + Si agrega paquetes que imponen demasiada presión computacional en el servidor, el rendimiento se verá afectado.

  + En un entorno de SQL Server protegido, puede que desee evitar lo siguiente:
    + Paquetes que requieren acceso a la red
    + Paquetes que requieren acceso al sistema de archivos elevado
    + Paquetes usados para el desarrollo web u otras tareas que no se benefician al ejecutarse dentro de SQL Server

## <a name="install-sqlmlutils-on-the-client-computer"></a>Instalación de sqlmlutils en el equipo cliente

Para usar **sqlmlutils**, primero debe instalarlo en el equipo cliente que usa para conectarse a SQL Server.

1. Descargue el archivo zip de **sqlmlutils** más https://github.com/Microsoft/sqlmlutils/tree/master/Python/dist reciente desde el equipo cliente. No descomprima el archivo.

1. Abra un **símbolo del sistema** y ejecute el siguiente comando para instalar el paquete **sqlmlutils** . Reemplace la ruta de acceso completa al archivo zip de **sqlmlutils** que descargó; en este ejemplo se `c:\temp\sqlmlutils_0.6.0.zip`da por supuesto que el archivo descargado es.

   ```console
   pip install --upgrade --upgrade-strategy only-if-needed c:\temp\sqlmlutils_0.6.0.zip
   ```

## <a name="add-a-python-package-on-sql-server"></a>Agregar un paquete de Python en SQL Server

En el ejemplo siguiente, agregará el paquete de [herramientas de texto](https://pypi.org/project/text-tools/) a SQL Server.

### <a name="add-the-package-online"></a>Agregar el paquete en línea

Si el equipo cliente que usa para conectarse a SQL Server tiene acceso a Internet, puede usar **sqlmlutils** para buscar el paquete de **herramientas de texto** y las dependencias a través de Internet y, a continuación, instalar el paquete en una instancia de SQL Server de forma remota.

1. En el equipo cliente, Abra **Python** o un entorno de Python.

1. Use los comandos siguientes para instalar el paquete **de herramientas de texto** . Sustituya su propia información de conexión de base de datos de SQL Server.

   ```python
   import sqlmlutils
   connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="yoursqluser", pwd="yoursqlpassword")
   sqlmlutils.SQLPackageManager(connection).install("text-tools")
   ```

### <a name="add-the-package-offline"></a>Agregar el paquete sin conexión

Si el equipo cliente que usa para conectarse a SQL Server no tiene conexión a Internet, puede usar **PIP** en un equipo con acceso a Internet para descargar el paquete y los paquetes dependientes en una carpeta local. A continuación, copie la carpeta en el equipo cliente en el que puede instalar el paquete sin conexión.

#### <a name="on-a-computer-with-internet-access"></a>En un equipo con acceso a Internet

1. Abra un **símbolo del sistema** y ejecute el siguiente comando para crear una carpeta local que contenga el paquete **de herramientas de texto** . En este ejemplo se crea `c:\temp\text-tools`la carpeta.

   ```command
   pip download text-tools -d c:\temp\text-tools
   ```

1. Copie la `text-tools` carpeta en el equipo cliente. En el ejemplo siguiente se da por supuesto `c:\temp\packages\text-tools`que lo copió en.

#### <a name="on-the-client-computer"></a>En el equipo cliente

Use **sqlmlutils** para instalar cada paquete (archivo WHL) que encuentre en la carpeta local que ha creado **PIP** . No importa en qué orden se instalan los paquetes.

En este ejemplo, **Text-Tools** no tiene dependencias, por lo que solo hay un archivo de `text-tools` la carpeta que se va a instalar. Por el contrario, un paquete como **scikit-Plot** tiene 11 dependencias, por lo que encontraría 12 archivos en la carpeta (el paquete **scikit-Plot** y los 11 paquetes dependientes) y debe instalar cada uno de ellos.

Ejecute el siguiente script de Python. Sustituya su propia información de conexión de base de datos de SQL Server y la ruta de acceso y el nombre de archivo reales del paquete. Repita la `sqlmlutils.SQLPackageManager` instrucción para cada archivo de paquete de la carpeta.

```python
import sqlmlutils
connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="yoursqluser", pwd="yoursqlpassword")
sqlmlutils.SQLPackageManager(connection).install("c:/temp/packages/text-tools/text_tools-1.0.0-py3-none-any.whl")
```

## <a name="use-the-package-in-sql-server"></a>Usar el paquete en SQL Server

Ahora puede usar el paquete en un script de Python en SQL Server. Por ejemplo:

```python
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
from text_tools.finders import find_best_string
corpus = "Lorem Ipsum text"
query = "Ipsum"
first_match = find_best_string(query, corpus)
print(first_match)
  '
```

## <a name="remove-the-package-from-sql-server"></a>Quitar el paquete de SQL Server

Si desea quitar el paquete de **herramientas de texto** , use el siguiente comando de Python en el equipo cliente, usando la misma variable de conexión que definió anteriormente.

```python
sqlmlutils.SQLPackageManager(connection).uninstall("text-tools")
```

## <a name="see-also"></a>Vea también

+ Para ver información sobre los paquetes de Python instalados en SQL Server Machine Learning Services, consulte [obtención de información de paquetes de Python](../package-management/python-package-information.md).

+ Para obtener información sobre la instalación de paquetes de R en SQL Server Machine Learning Services, consulte [instalar nuevos paquetes de r en SQL Server](../r/install-additional-r-packages-on-sql-server.md).
