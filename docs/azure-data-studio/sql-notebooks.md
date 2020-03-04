---
title: Procedimiento para usar cuadernos SQL
titleSuffix: Azure Data Studio
description: Procedimiento para usar cuadernos SQL en Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: achatter; alayu; maghan; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.custom: seodec18
ms.date: 06/28/2019
ms.openlocfilehash: b2651dd2d95f0fb8b5aba37b1d755bc26a781dde
ms.sourcegitcommit: 844793cd1c058e6bba136f050734e7dc62024a82
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/25/2020
ms.locfileid: "77575372"
---
# <a name="how-to-use-notebooks-in-azure-data-studio"></a>Uso de cuadernos en Azure Data Studio

En este artículo se explica cómo iniciar la experiencia de Notebook en Azure Data Studio y cómo empezar a crear cuadernos propios. También se muestra cómo escribir cuadernos con distintos kernels.

## <a name="connect-to-sql-server"></a>Conectar a SQL Server

Puede conectarse al tipo de conexión de Microsoft SQL Server en Azure Data Studio.
En Azure Data Studio, también puede presionar F1 y hacer clic en **Nueva conexión**  y conectarse a SQL Server.

![image1](media/sql-notebooks/connection-info.png)

## <a name="launch-notebooks"></a>Inicio de los cuadernos

Hay varias maneras de iniciar un nuevo cuaderno.

1. Vaya al **menú Archivo** en Azure Data Studio y haga clic en **Nuevo cuaderno**.

    ![image3](media/sql-notebooks/file-new-notebook.png)

2. Haga clic con el botón derecho en la conexión **SQL Server** e inicie **Nuevo cuaderno**. 
    ![image3](media/sql-notebooks/server-new-notebook.png)

3. Abra la paleta de comandos (**Ctrl + Mayús + P**) y, luego, escriba **Nuevo cuaderno**. Se abre un nuevo archivo denominado `Notebook-1.ipynb`.

## <a name="supported-kernels-and-attach-to-context"></a>Kernels admitidos y asociación al contexto

La instalación de Notebooks en Azure Data Studio es compatible de forma nativa con el kernel de SQL. Si es desarrollador de SQL y quiere usar Notebooks, este sería el kernel elegido.

El kernel de SQL también se puede usar para conectarse a instancias de servidor de PostgreSQL. Si es desarrollador de PostgreSQL y quiere conectarse al servidor de PostgreSQL, descargue la [**extensión de PostgreSQL**](postgres-extension.md) en el Marketplace de extensiones de Azure Data Studio.

![image7](media/sql-notebooks/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>SQL Kernel

En las celdas de código del cuaderno, de forma similar al editor de consultas, se admite la experiencia de codificación moderna de SQL que facilita las tareas diarias con características integradas, como un editor de SQL enriquecido, IntelliSense y fragmentos de código integrados. Los fragmentos de código permiten generar la sintaxis SQL adecuada para crear bases de datos, tablas, vistas, procedimientos almacenados, etc., y para actualizar los objetos de base de datos existentes. Use fragmentos de código para crear rápidamente copias de la base de datos con fines de desarrollo o prueba y para generar y ejecutar scripts.

Haga clic en **Ejecutar** para ejecutar cada celda.

Kernel de SQL para conectar a la instancia de SQL Server

![image7](media/sql-notebooks/intellisense-code-cell.png)

Resultados de la consulta

![image19](media/sql-notebooks/sql-cell-results.png)

Kernel de SQL para conectar a la instancia de servidor de PostgreSQL 

![image18](media/sql-notebooks/pgsql-code-cell.png)

Resultados de la consulta

![image20](media/sql-notebooks/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>Configuración de Python para Notebooks

Al seleccionar cualquiera de los otros kernels distintos de SQL en la lista desplegable de kernels, se le pide que **configure Python para Notebooks**. Las dependencias de Notebooks se instalan en una ubicación especificada, pero puede decidir si quiere establecer la ubicación de instalación. Esta instalación puede tardar algún tiempo y se recomienda no cerrar la aplicación hasta que se complete la instalación. Una vez que esté completada la instalación, podrá empezar a escribir código en el lenguaje admitido.

![image21](media/sql-notebooks/configure-python.png)

Una vez que la instalación se realice correctamente, aparecerá una notificación en el historial de tareas junto con la ubicación del servidor back-end de Jupyter que se ejecuta en el terminal de salida.

![image22](media/sql-notebooks/jupyter-backend.png)

|Kernel|Descripción
|:-----|:-----
| SQL Kernel | Escribe código SQL destinado a la base de datos relacional.
|Kernel de PySpark3 y PySpark| Escribe código de Python mediante un proceso de Spark desde el clúster.
|Kernel de Spark|Escribe código de Scala y R mediante un proceso de Spark desde el clúster.
|Python Kernel|Escribe código de Python para el desarrollo local.

`Attach to` proporciona el contexto para que el kernel se asocie. Si usa el kernel de SQL, puede usar `Attach to` para cualquiera de las instancias de SQL Server.

Si usa el kernel de Python3, `Attach to` es `localhost`. Puede usar este kernel para el desarrollo local de Python.

Cuando esté conectado al clúster de macrodatos de SQL Server 2019, el elemento `Attach to` predeterminado es ese punto final del clúster que permite enviar código de Python, Scala y R mediante el proceso de Spark del clúster.

### <a name="code-cells-and-markdown-cells"></a>Celdas de código y celdas de Markdown

Agregue una nueva celda de código haciendo clic en el comando **+Código** de la barra de herramientas.

Agregue una nueva celda de texto haciendo clic en el comando **+Texto** de la barra de herramientas.

![image8](media/sql-notebooks/notebook-toolbar.png)

La celda cambia al modo de edición; ahora escriba Markdown para ver la versión preliminar al mismo tiempo.

![image9](media/sql-notebooks/notebook-markdown-cell.png)

Al hacer clic fuera de la celda de texto, se muestra el texto de Markdown.

![image10](media/sql-notebooks/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>De confianza y No de confianza

El valor predeterminado de los cuadernos abiertos en Azure Data Studio es **De confianza**.

Si abre un cuaderno desde algún otro origen, se abre en modo **No de confianza** y, luego, se puede convertir a **De confianza**.

### <a name="save"></a>Save

Para guardar el cuaderno, presione **Ctrl + S** o haga clic en los comandos **Guardar archivo**, **Guardar archivo como...** y **Guardar todo** desde el menú archivo y los comandos **Archivo: Guardar** especificados en la paleta de comandos.

### <a name="pyspark3pyspark-kernel"></a>Kernel de Pyspark3/PySpark

Elija `PySpark Kernel` y el tipo de celda en el código siguiente.

Haga clic en **Ejecutar**.

La aplicación Spark se inicia y devuelve el siguiente resultado:

![image12](media/sql-notebooks/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Kernel de Spark | Lenguaje Scala

Elija `Spark|Scala Kernel` y el tipo de celda en el código siguiente.

![image13](media/sql-notebooks/spark-scala.png)

También puede ver las "Opciones de celda" al hacer clic en el icono de opciones que aparece bajo:

![image14](media/sql-notebooks/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Kernel de Spark | Lenguaje R

Elija Spark | R en la lista desplegable de los kernels. En la celda, escriba o pegue el código. Haga clic en **Ejecutar** para ver la siguiente salida.

![image15](media/sql-notebooks/spark-r.png)

### <a name="local-python-kernel"></a>Kernel local de Python

Elija el kernel local de Python y el tipo de celda en:

![image16](media/sql-notebooks/local-python.png)

## <a name="manage-packages"></a>Administración de paquetes

Uno de los aspectos que se han optimizado para el desarrollo local de Python es la capacidad de instalar paquetes que los clientes necesitan para sus escenarios. De forma predeterminada, se incluyen los paquetes comunes como `pandas`, `numpy`, etc., pero si espera un paquete que no está incluido, escriba el código siguiente en la celda del cuaderno:

```python
import <package-name>
```

Al ejecutar este comando, se devuelve `Module not found`. Si el paquete existe, no aparece el error.

Si devuelve un error `Module not Found`, haga clic en **Administrar paquetes** para iniciar el asistente. 

![image17](media/sql-notebooks/manage-packages.png)

En este asistente puede ver los paquetes **instalados**. Puede buscar en la lista y en la versión asociada de cada uno de estos paquetes. Si necesita desinstalar cualquiera de estos paquetes, puede hacer clic en uno de los paquetes y, después, hacer clic en la opción **Desinstalar los paquetes seleccionados**.

También puede hacer clic en **Agregar nuevos paquetes** para **Buscar** un paquete determinado, elegir la versión relacionada y hacer clic en **Instalar**. De forma predeterminada, se selecciona la versión más reciente del paquete buscado.

Una vez instalado el paquete, se puede ir a la celda del cuaderno y escribir el comando siguiente:

```python
import <package-name>
```

Si necesita desinstalar cualquiera de estos paquetes, puede hacer clic en uno o varios paquetes y luego en la opción **Desinstalar los paquetes seleccionados**.

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre cómo trabajar con un cuaderno existente, vea [Cómo administrar cuadernos en Azure Data Studio](https://docs.microsoft.com/sql/big-data-cluster/notebooks-how-to-manage?view=sqlallproducts-allversions).