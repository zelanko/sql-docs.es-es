---
title: Cómo usar cuadernos de SQL en Azure Data Studio
titleSuffix: Azure Data Studio
description: Obtenga información sobre cómo usar cuadernos de SQL en Azure Data Studio
ms.custom: seodec18
ms.date: 06/28/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: achatter; alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 9af2e04a3973eddfcd714c7968c35e544302aba9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959261"
---
# <a name="how-to-use-notebooks-in-azure-data-studio"></a>Uso de cuadernos en Azure Data Studio

En este artículo se describe cómo iniciar la experiencia del cuaderno en Azure Data Studio y cómo empezar a crear sus propios cuadernos. También muestra cómo escribir utilizando diferentes kernels de cuadernos.


## <a name="connect-to-sql-server"></a>Conexión con SQL Server

Puede conectarse al tipo de conexión de Microsoft SQL Server en Azure Data Studio.
En Azure Data Studio, también puede presionar F1 y haga clic en **nueva conexión** y conectarse a SQL Server.

![Image1](media/sql-notebooks/connection-info.png)

## <a name="launch-notebooks"></a>Iniciar blocs de notas

Hay varias formas de iniciar un nuevo cuaderno.

1. Vaya a la **menú archivo** en Azure Data Studio y, a continuación, haga clic en **nuevo cuaderno**.

    ![image3](media/sql-notebooks/file-new-notebook.png)

3. Haga clic con el botón derecho en el **SQL Server** conexión y, a continuación, inicie **nuevo cuaderno**. 
    ![image3](media/sql-notebooks/server-new-notebook.png)

4. Abra la paleta de comandos (**Ctrl + Mayús + P**)) y, a continuación, escriba en **nuevo cuaderno**. Un nuevo archivo denominado `Notebook-1.ipynb` se abre.

## <a name="supported-kernels-and-attach-to-context"></a>Admite los kernels y asociar al contexto

La instalación de Bloc de notas en Azure Data Studio admite de forma nativa del núcleo de SQL. Si es un desarrollador SQL y le gustaría utilizar blocs de notas, entonces esto sería elegido Kernel. 

El núcleo de SQL también puede utilizarse para conectarse a instancias de servidor de PostgreSQL. Si es un desarrollador de PostgreSQL y le gustaría conectarse al servidor de PostgreSQL, a continuación, descargue el [ **PostgreSQL extensión** ](postgres-extension.md) en el marketplace de extensiones de Azure Data Studio.

![image7](media/sql-notebooks/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>Núcleo SQL

En las celdas de código en el Bloc de notas, similar a nuestro editor de consultas, se admite SQL moderna experiencia que facilita sus tareas diarias con características integradas, como un editor SQL enriquecido, IntelliSense y fragmentos de código integrados de codificación. Fragmentos de código le permiten generar la sintaxis correcta de SQL para crear bases de datos, tablas, vistas, procedimientos almacenados, etc. y para actualizar los objetos de base de datos existente. Usar fragmentos de código para crear rápidamente copias de la base de datos para el desarrollo o con fines de prueba y para generar y ejecutar scripts.

Haga clic en **ejecutar** para ejecutar cada celda.

Núcleo de SQL para conectarse a la instancia de SQL Server

![image7](media/sql-notebooks/intellisense-code-cell.png)

Resultados de la consulta

![Image19](media/sql-notebooks/sql-cell-results.png)

Núcleo de SQL para conectarse a la instancia del servidor de PostgreSQL 

![Image18](media/sql-notebooks/pgsql-code-cell.png)

Resultados de la consulta

![Image20](media/sql-notebooks/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>Configurar Python para cuadernos

Al seleccionar cualquiera de los kernels aparte de SQL en la lista desplegable de kernel, esto le pide que **configurar Python para cuadernos de**. Las dependencias de Bloc de notas se instalan en una ubicación especificada, pero puede decidir si va a establecer la ubicación de instalación. Esta instalación puede tardar algún tiempo y se recomienda no cerrar la aplicación hasta que finalice la instalación. Una vez finalizada la instalación, puede empezar a escribir código en el idioma.

![Image21](media/sql-notebooks/configure-python.png)

Una vez que la instalación se realiza correctamente, encontrará una notificación en el historial de tareas junto con la ubicación del servidor de back-end de Jupyter que se ejecuta en el Terminal de salida.

![Image22](media/sql-notebooks/jupyter-backend.png)

|Kernel|Descripción
|:-----|:-----
| Núcleo SQL | Escribir código de SQL destinado a la base de datos relacional.
|PySpark3 y Kernel PySpark| Escribir código de Python mediante el proceso de Spark del clúster.
|Kernel de Spark|Escribir código de Scala y R mediante el proceso de Spark del clúster.
|Python Kernel|Escribir código de Python para el desarrollo local.

`Attach to` proporciona el contexto para el Kernel adjuntar. Si usas el núcleo de SQL, puede `Attach to` cualquiera de las instancias de SQL Server.

Si usa el Kernel de Python3 el `Attach to` es `localhost`. Puede usar este kernel para el desarrollo de Python local.

Cuando esté conectado al clúster de SQL Server 2019 datos de gran tamaño, el valor predeterminado `Attach to` es ese punto de conexión del clúster y le permitirá enviar código de Python, Scala y R mediante el proceso de Spark del clúster.

### <a name="code-cells-and-markdown-cells"></a>Celdas de código y Markdown

Agregar una nueva celda de código haciendo clic en el **+ código** comando en la barra de herramientas.

Agregar una nueva celda de texto haciendo clic en el **+ texto** comando en la barra de herramientas.

![image8](media/sql-notebooks/notebook-toolbar.png)

La celda cambia al modo de edición y ahora escriba markdown y verá la vista previa a la vez

![image9](media/sql-notebooks/notebook-markdown-cell.png)

Hacer clic fuera de la celda de texto se mostrará el texto de markdown.

![Image10](media/sql-notebooks/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>Confianza y que no son de confianza

Blocs de notas abierto en Azure Data Studio son predeterminados **confianza**.

Si abre un bloc de notas de algún otro origen, se abrirá en **que no son de confianza** modo y, a continuación, se puede realizar **confianza**.

### <a name="save"></a>Save 

Puede guardar el cuaderno por **CTRL+s** o haciendo clic en el **Guardar archivo**, **Guardar como...**  y **archivo Guardar todo** comandos en el menú archivo y **archivo: Guardar** los comandos escritos en la paleta de comandos.

### <a name="pyspark3pyspark-kernel"></a>Kernel Pyspark3/PySpark

Elija el `PySpark Kernel` y en el tipo de celda en el código siguiente.

Haga clic en **Ejecutar**.

La aplicación de Spark se inicia y devuelve el siguiente resultado:

![Image12](media/sql-notebooks/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Kernel de Spark | Lenguaje de scala

Elija el `Spark|Scala Kernel` y en el tipo de celda en el código siguiente.

![Image13](media/sql-notebooks/spark-scala.png)

También puede ver las opciones de"celda" al hacer clic en el icono de opciones siguiente:

![Image14](media/sql-notebooks/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Kernel de Spark | Lenguaje R

Elija el Spark | R en la lista desplegable de los kernels. En la celda, escriba o pegue el código. Haga clic en **ejecutar** para ver el resultado siguiente.

![Image15](media/sql-notebooks/spark-r.png)

### <a name="local-python-kernel"></a>Kernel de Python local

Elija el Kernel de Python local y en el tipo de celda:

![Image16](media/sql-notebooks/local-python.png)

## <a name="manage-packages"></a>Administración de paquetes
Una de las cosas que hemos optimizado para el desarrollo de Python local era incluyen la capacidad para instalar los paquetes que los clientes tendrían para sus escenarios. De forma predeterminada, se incluyen los paquetes comunes como `pandas`, `numpy` etc., pero si se espera un paquete que no se incluye a continuación, escribir el código siguiente en la celda del Bloc de notas: 

```python
import <package-name>
```

Al ejecutar este comando, `Module not found` se devuelve. Si el paquete no existe, no obtendrá el error.

Si devuelve un `Module not Found` error y, a continuación, haga clic en **administrar paquetes** para iniciar la experiencia de asistente. 

![Image17](media/sql-notebooks/manage-packages.png)

En este asistente podrá ver el **instalado** paquetes. Puede buscar a través de la lista y la versión asociada de cada uno de estos paquetes. Si necesita **desinstalar** cualquiera de estos paquetes, a continuación, puede hacer clic en uno de los paquetes y, a continuación, haga clic en el **desinstalar los paquetes seleccionados** opción.

También podrá hacer clic en **Agregar nuevo** paquetes a **búsqueda** para un paquete determinado, elija la versión relacionada y haga clic en **instalar**. De forma predeterminada, se selecciona la versión más reciente del paquete de búsqueda. 

Después de instalar el paquete, debe ir en la celda del Bloc de notas y escriba en el siguiente comando:

```python
import <package-name>
```

Si necesita **desinstalar** cualquiera de estos paquetes, a continuación, puede hacer clic en uno o varios paquetes y, a continuación, haga clic en el **desinstalar los paquetes seleccionados** opción.

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre cómo trabajar con un bloc de notas existente, consulte [cómo administrar los cuadernos en Azure Data Studio](https://docs.microsoft.com/sql/big-data-cluster/notebooks-how-to-manage?view=sqlallproducts-allversions).