---
title: Ejecutar blocs de notas en Azure Data Studio
titleSuffix: SQL Server big data clusters
description: Este artículo explica cómo ejecutar Jupyter Notebook en Azure Data Studio conectado a un clúster de macrodatos de SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: a220b78fe93b286837e0e235b881ffd1a612e512
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58859976"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>Uso de cuadernos en versión preliminar de SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo iniciar la experiencia del cuaderno en Azure Data Studio y cómo empezar a crear sus propios cuadernos. También muestra cómo escribir utilizando diferentes kernels de cuadernos.

## <a name="connect-to-sql-server"></a>Conectar a SQL Server

Puede conectarse al tipo de conexión de Microsoft SQL Server en Azure Data Studio.
En Azure Data Studio, también puede presionar F1 y haga clic en **nueva conexión** y conectarse a SQL Server.

![Información de conexión](media/notebooks-guidance/connection-info.png)

## <a name="launch-notebooks"></a>Iniciar blocs de notas

Hay varias formas de iniciar un nuevo cuaderno.

- Vaya a la **menú archivo** en Azure Data Studio y, a continuación, haga clic en **nuevo cuaderno**.

    ![Nuevo cuaderno](media/notebooks-guidance/file-new-notebook.png)

- Haga clic con el botón derecho en el **SQL Server** conexión y, a continuación, inicie **nuevo cuaderno**.

    ![Nuevo cuaderno](media/notebooks-guidance/server-new-notebook.png)

- Abra la paleta de comandos (**Ctrl + Mayús + P**)) y, a continuación, escriba en **nuevo cuaderno**. Un nuevo archivo denominado `Notebook-1.ipynb` se abre.

## <a name="supported-kernels-and-attach-to-context"></a>Admite los kernels y asociar al contexto

La instalación de Bloc de notas en Azure Data Studio admite de forma nativa del núcleo de SQL. Si es un desarrollador SQL y le gustaría utilizar blocs de notas, entonces esto sería elegido Kernel. 

El núcleo de SQL también puede utilizarse para conectarse a instancias de servidor de PostgreSQL. Si es un desarrollador de PostgreSQL y le gustaría conectarse al servidor de PostgreSQL, a continuación, descargue el [ **PostgreSQL extensión** ](../azure-data-studio/postgres-extension.md) en el marketplace de extensiones de Azure Data Studio.

![Conexión de PostgreSQL](media/notebooks-guidance/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>SQL Kernel

En las celdas de código en el Bloc de notas, similar a nuestro editor de consultas, se admite SQL moderna experiencia que facilita sus tareas diarias con características integradas, como un editor SQL enriquecido, IntelliSense y fragmentos de código integrados de codificación. Fragmentos de código le permiten generar la sintaxis correcta de SQL para crear bases de datos, tablas, vistas, procedimientos almacenados, etc. y para actualizar los objetos de base de datos existente. Usar fragmentos de código para crear rápidamente copias de la base de datos para el desarrollo o con fines de prueba y para generar y ejecutar scripts.

Haga clic en **ejecutar** para ejecutar cada celda.

Núcleo de SQL para conectarse a la instancia de SQL Server

![SQL Kernel](media/notebooks-guidance/intellisense-code-cell.png)

Resultados de la consulta

![Resultados de la consulta](media/notebooks-guidance/sql-cell-results.png)

Núcleo de SQL para conectarse a la instancia del servidor de PostgreSQL 

![Conexión de PostgreSQL](media/notebooks-guidance/pgsql-code-cell.png)

Resultados de la consulta

![Resultados de la consulta](media/notebooks-guidance/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>Configurar Python para cuadernos

Al seleccionar cualquiera de los kernels aparte de SQL en la lista desplegable de kernel, esto le pide que **configurar Python para cuadernos de**. Las dependencias de Bloc de notas se instalan en una ubicación especificada, pero puede decidir si va a establecer la ubicación de instalación. Esta instalación puede tardar algún tiempo y se recomienda no cerrar la aplicación hasta que finalice la instalación. Una vez finalizada la instalación, puede empezar a escribir código en el idioma.

![Configurar python](media/notebooks-guidance/configure-python.png)

Una vez que la instalación se realiza correctamente, encontrará una notificación en el historial de tareas junto con la ubicación del servidor de back-end de Jupyter que se ejecuta en el Terminal de salida.

![Back-end de Jupyter](media/notebooks-guidance/jupyter-backend.png)

|Kernel|Descripción
|:-----|:-----
| SQL Kernel | Escribir código de SQL destinado a la base de datos relacional.
|PySpark3 y Kernel PySpark| Escribir código de Python mediante el proceso de Spark del clúster.
|Spark Kernel|Escribir código de Scala y R mediante el proceso de Spark del clúster.
|Python Kernel|Escribir código de Python para el desarrollo local.

`Attach to` proporciona el contexto para el Kernel adjuntar. Si usas el núcleo de SQL, puede `Attach to` cualquiera de las instancias de SQL Server.

Si usa el Kernel de Python3 el `Attach to` es `localhost`. Puede usar este kernel para el desarrollo de Python local.

Cuando esté conectado al clúster de SQL Server 2019 datos de gran tamaño, el valor predeterminado `Attach to` es ese punto de conexión del clúster y le permitirá enviar código de Python, Scala y R mediante el proceso de Spark del clúster.

### <a name="code-cells-and-markdown-cells"></a>Celdas de código y Markdown

Agregar una nueva celda de código haciendo clic en el **+ código** comando en la barra de herramientas.

Agregar una nueva celda de texto haciendo clic en el **+ texto** comando en la barra de herramientas.

![Barra de herramientas del Bloc de notas](media/notebooks-guidance/notebook-toolbar.png)

La celda cambia al modo de edición y ahora escriba markdown y verá la vista previa a la vez

![Celda de markdown](media/notebooks-guidance/notebook-markdown-cell.png)

Hacer clic fuera de la celda de texto se mostrará el texto de markdown.

![Text v markdownu](media/notebooks-guidance/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>Confianza y que no son de confianza

Blocs de notas abierto en Azure Data Studio son predeterminados **confianza**.

Si abre un bloc de notas de algún otro origen, se abrirá en **que no son de confianza** modo y, a continuación, se puede realizar **confianza**.

### <a name="save"></a>Guardar

Puede guardar el cuaderno por **CTRL+s** o haciendo clic en el **Guardar archivo**, **Guardar como...**  y **archivo Guardar todo** comandos en el menú archivo y **archivo: Guardar** los comandos escritos en la paleta de comandos.

### <a name="pyspark3pyspark-kernel"></a>Kernel Pyspark3/PySpark

Elija el `PySpark Kernel` y en el tipo de celda en el código siguiente.

Haga clic en **Ejecutar**.

La aplicación de Spark se inicia y devuelve el siguiente resultado:

![Aplicación de Spark](media/notebooks-guidance/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Kernel de Spark | Lenguaje de scala

Elija el `Spark|Scala Kernel` y en el tipo de celda en el código siguiente.

![Spark en Scala](media/notebooks-guidance/spark-scala.png)

También puede ver las opciones de"celda" al hacer clic en el icono de opciones siguiente:

![Opciones de celda](media/notebooks-guidance/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Kernel de Spark | Lenguaje R

Elija el Spark | R en la lista desplegable de los kernels. En la celda, escriba o pegue el código. Haga clic en **ejecutar** para ver el resultado siguiente.

![Spark, R](media/notebooks-guidance/spark-r.png)

### <a name="local-python-kernel"></a>Kernel de Python local

Elija el Kernel de Python local y en el tipo de celda:

![Python local](media/notebooks-guidance/local-python.png)

## <a name="manage-packages"></a>Administración de paquetes

Una de las cosas que hemos optimizado para el desarrollo de Python local era incluyen la capacidad para instalar los paquetes que los clientes tendrían para sus escenarios. De forma predeterminada, se incluyen los paquetes comunes como `pandas`, `numpy` etc., pero si se espera un paquete que no se incluye a continuación, escribir el código siguiente en la celda del Bloc de notas: 

```python
import <package-name>
```

Al ejecutar este comando, `Module not found` se devuelve. Si el paquete no existe, no obtendrá el error.

Si devuelve un `Module not Found` error y, a continuación, haga clic en **administrar paquetes** para iniciar el terminal. Ahora puede instalar los paquetes localmente. Use los siguientes comandos para instalar los paquetes:

```bash
./pip install <package-name>
```

   > [!Tip]
   > Siga las instrucciones que aparecen en la ventana de Terminal para instalar paquetes en Mac. 

Después de instalar el paquete, debe ir en la celda del Bloc de notas y escriba en el siguiente comando:

```python
import <package-name>
```

Para desinstalar un paquete, use el siguiente comando desde el terminal:

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre cómo trabajar con un bloc de notas existente, consulte [cómo administrar los cuadernos en Azure Data Studio](notebooks-how-to-manage.md).