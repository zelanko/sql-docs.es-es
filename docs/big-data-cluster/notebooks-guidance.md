---
title: Ejecución de cuadernos en Azure Data Studio
titleSuffix: SQL Server big data clusters
description: En este artículo se explica cómo ejecutar cuadernos de Jupyter en Azure Data Studio conectado a un clúster de macrodatos de SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 05/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 166964f97f5201d906ea2d1f6262b7a221eb2cba
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958297"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>Cómo usar los cuadernos en la versión preliminar de SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se explica cómo iniciar la experiencia de Notebooks en la última versión de [**Azure Data Studio**](../azure-data-studio/download.md) y cómo empezar a crear cuadernos propios. También se muestra cómo escribir cuadernos con distintos kernels.

## <a name="connect-to-sql-server"></a>Conectar a SQL Server

Puede conectarse al tipo de conexión de Microsoft SQL Server en Azure Data Studio.
En Azure Data Studio, también puede presionar F1 y hacer clic en **Nueva conexión**  y conectarse a SQL Server.

![Información de conexión](media/notebooks-guidance/connection-info.png)

## <a name="launch-notebooks"></a>Inicio de los cuadernos

Hay varias maneras de iniciar un nuevo cuaderno.

- Vaya al **menú Archivo** en Azure Data Studio y haga clic en **Nuevo cuaderno**.

    ![Nuevo cuaderno](media/notebooks-guidance/file-new-notebook.png)

- Haga clic con el botón derecho en la conexión **SQL Server** e inicie **Nuevo cuaderno**.

    ![Nuevo cuaderno](media/notebooks-guidance/server-new-notebook.png)

- Abra la paleta de comandos (**Ctrl + Mayús + P**) y, luego, escriba **Nuevo cuaderno**. Se abre un nuevo archivo denominado `Notebook-1.ipynb`.

## <a name="supported-kernels-and-attach-to-context"></a>Kernels admitidos y asociación al contexto

La instalación de Notebooks en Azure Data Studio es compatible de forma nativa con el kernel de SQL. Si es desarrollador de SQL y quiere usar Notebooks, este sería el kernel elegido. 

El kernel de SQL también se puede usar para conectarse a instancias de servidor de PostgreSQL. Si es desarrollador de PostgreSQL y quiere conectar los cuadernos al servidor de PostgreSQL, descargue la [**extensión PostgreSQL**](../azure-data-studio/postgres-extension.md) en la extensión Azure Data Studio e inicie **Nuevo cuaderno** para abrir una instancia de cuaderno para conectarse al servidor de PostgreSQL.

![Conexión de PostgreSQL](media/notebooks-guidance/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>Kernel de SQL

En las celdas de código del cuaderno, de forma similar al editor de consultas, se admite la experiencia de codificación moderna de SQL que facilita las tareas diarias con características integradas, como un editor de SQL enriquecido, IntelliSense y fragmentos de código integrados. Los fragmentos de código permiten generar la sintaxis SQL adecuada para crear bases de datos, tablas, vistas, procedimientos almacenados, etc., y para actualizar los objetos de base de datos existentes. Use fragmentos de código para crear rápidamente copias de la base de datos con fines de desarrollo o prueba y para generar y ejecutar scripts.

Haga clic en **Ejecutar** para ejecutar cada celda.

Kernel de SQL para conectar a la instancia de SQL Server

![Kernel de SQL](media/notebooks-guidance/intellisense-code-cell.png)

Resultados de la consulta

![Resultados de la consulta](media/notebooks-guidance/sql-cell-results.png)

Kernel de SQL para conectar a la instancia de servidor de PostgreSQL 

![Conexión de PostgreSQL](media/notebooks-guidance/pgsql-code-cell.png)

Resultados de la consulta

![Resultados de la consulta](media/notebooks-guidance/pgsql-cell-results.png)

Si quiere agregar celdas de texto al cuaderno existente asociado al kernel de SQL, haga clic en el comando **+Texto** de la barra de herramientas.

![Barra de herramientas de los cuaderno](media/notebooks-guidance/notebook-toolbar.png)

La celda cambia al modo de edición; ahora escriba Markdown para ver la versión preliminar al mismo tiempo.

![Celda de Markdown](media/notebooks-guidance/notebook-markdown-cell.png)

Al hacer clic fuera de la celda de texto, se muestra el texto de Markdown.

![Texto de Markdown](media/notebooks-guidance/notebook-markdown-preview.png)


### <a name="configure-python-for-notebooks"></a>Configuración de Python para Notebooks

Al seleccionar cualquiera de los otros kernels distintos de SQL en la lista desplegable de kernels, se le pide que **configure Python para Notebooks**. Las dependencias de Notebooks se instalan en una ubicación especificada, pero puede decidir si quiere establecer la ubicación de instalación. Esta instalación puede tardar algún tiempo y se recomienda no cerrar la aplicación hasta que se complete la instalación. Una vez finalizada la instalación, puede empezar a escribir código en el lenguaje admitido.

![Configuración de Python](media/notebooks-guidance/configure-python.png)

Una vez que la instalación se realiza correctamente, aparece una notificación en el historial de tareas junto con la ubicación del servidor back-end de Jupyter que se ejecuta en el terminal de salida.

![Back-end de Jupyter](media/notebooks-guidance/jupyter-backend.png)

|Kernel|Descripción
|:-----|:-----
| SQL Kernel | Escribe código SQL destinado a la base de datos relacional.
|Kernel de PySpark3 y PySpark| Escribe código de Python mediante un proceso de Spark desde el clúster.
|Kernel de Spark|Escribe código de Scala y R mediante un proceso de Spark desde el clúster.
|Python Kernel|Escribe código de Python para el desarrollo local.

`Attach to` proporciona el contexto para que el kernel se asocie. Si usa el kernel de SQL, puede `Attach to` cualquiera de las instancias de SQL Server.

Si usa el kernel de Python3, `Attach to` es `localhost`. Puede usar este kernel para el desarrollo local de Python.

Cuando esté conectado al clúster de macrodatos de SQL Server 2019, el elemento `Attach to` predeterminado es ese punto final del clúster y le permite enviar código de Python, Scala y R mediante el proceso de Spark del clúster.

### <a name="code-cells-and-markdown-cells"></a>Celdas de código y celdas de Markdown

Agregue una nueva celda de código haciendo clic en el comando **+Código** de la barra de herramientas.

Agregue una nueva celda de texto al hacer clic en el comando **+Texto** de la barra de herramientas.

![Barra de herramientas de los cuaderno](media/notebooks-guidance/notebook-toolbar.png)

La celda cambia al modo de edición; ahora escriba Markdown para ver la versión preliminar al mismo tiempo.

![Celda de Markdown](media/notebooks-guidance/notebook-markdown-cell.png)

Al hacer clic fuera de la celda de texto, se muestra el texto de Markdown.

![Texto de Markdown](media/notebooks-guidance/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>De confianza y No de confianza

El valor predeterminado de los cuadernos abiertos en Azure Data Studio es **De confianza**.

Si abre un cuaderno desde algún otro origen, se abre en modo **No de confianza** y, luego, se puede convertir a **De confianza**.

### <a name="run-cells"></a>Ejecución de celdas
Si quiere ejecutar todas las celdas del cuaderno, haga clic en el botón **Ejecutar celdas** de la barra de herramientas.

![Texto de Markdown](media/notebooks-guidance/run-cell.png)


### <a name="clear-results"></a>Borrar resultados

Si quiere borrar los resultados de todas las celdas ejecutadas del cuaderno, puede hacer clic en el botón **Borrar resultados** de la barra de herramientas.

![Texto de Markdown](media/notebooks-guidance/clear-results.png)

### <a name="save"></a>Guardar

Para guardar el cuaderno, realice una de las siguientes operaciones.

- Seleccione Ctrl + S
- Haga clic en **Archivo** > **Guardar**.
- Haga clic en **Archivo** > **Guardar como...** .
- Haga clic en **Archivo** > **Guardar todo**. 
- En la paleta de comandos, escriba **Archivo: Guardar**. 

### <a name="pyspark3pyspark-kernel"></a>Kernel de Pyspark3/PySpark

Elija `PySpark Kernel` y el tipo de celda en el código siguiente.

Haga clic en **Ejecutar**.

La aplicación Spark se inicia y devuelve el siguiente resultado:

![Aplicación Spark](media/notebooks-guidance/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Kernel de Spark | Lenguaje Scala

Elija `Spark|Scala Kernel` y el tipo de celda en el código siguiente.

![Spark Scala](media/notebooks-guidance/spark-scala.png)

También puede ver las "Opciones de celda" al hacer clic en el icono de opciones que aparece bajo:

![Opciones de celda](media/notebooks-guidance/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Kernel de Spark | Lenguaje R

Elija Spark | R en la lista desplegable de los kernels. En la celda, escriba o pegue el código. Haga clic en **Ejecutar** para ver la siguiente salida.

![Spark R](media/notebooks-guidance/spark-r.png)

### <a name="local-python-kernel"></a>Kernel local de Python

Elija el kernel local de Python y el tipo de celda en:

![Python local](media/notebooks-guidance/local-python.png)

## <a name="manage-packages"></a>Administración de paquetes

Uno de los aspectos que se han optimizado para el desarrollo local de Python es la capacidad de instalar paquetes que los clientes necesitan para sus escenarios. De forma predeterminada, se incluyen los paquetes comunes como `pandas`, `numpy`, etc., pero si espera un paquete que no está incluido, escriba el código siguiente en la celda del cuaderno: 

```python
import <package-name>
```

Al ejecutar este comando, se devuelve `Module not found`. Si el paquete existe, no aparece el error.

Si devuelve un error `Module not Found`, haga clic en **Administrar paquetes** para iniciar el terminal. Ahora puede instalar paquetes localmente. Use los comandos siguientes para instalar los paquetes:

```bash
./pip install <package-name>
```

   > [!Tip]
   > En Mac, siga las instrucciones de la ventana Terminal para instalar paquetes. 

Una vez instalado el paquete, debería poder ir a la celda del cuaderno y escribir el siguiente comando:

```python
import <package-name>
```

Para desinstalar un paquete, use el siguiente comando desde el terminal:

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre cómo trabajar con un cuaderno existente, vea [Cómo administrar cuadernos en Azure Data Studio](notebooks-how-to-manage.md).