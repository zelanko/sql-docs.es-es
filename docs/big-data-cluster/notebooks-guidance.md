---
title: Ejecutar blocs de notas en Azure Data Studio
titleSuffix: SQL Server 2019 big data clusters
description: Este artículo explica cómo ejecutar Jupyter Notebook en Azure Data Studio conneected a un clúster de macrodatos de SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/12/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 44ba203fcd7445add8fce00dd64913f85bcf4cc1
ms.sourcegitcommit: 11ab8a241a6d884b113b3cf475b2b9ed61ff00e3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161662"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>Uso de cuadernos en versión preliminar de SQL Server 2019

En este artículo se describe cómo iniciar Jupyter Notebooks en un clúster de macrodatos y cómo empezar a crear sus propios cuadernos. También muestra cómo enviar trabajos en el clúster.

## <a name="prerequisites"></a>Requisitos previos

Para usar los blocs de notas, debe instalar los requisitos previos siguientes:

- [Un clúster de macrodatos de SQL Server 2019](deployment-guidance.md)
- [Herramientas de SQL Server 2019 macrodatos](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
   - **kubectl**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-sql-server-big-data-cluster-end-point"></a>Conectarse al punto final de clúster de SQL Server datos de gran tamaño

Puede conectarse a diferentes puntos de conexión del clúster. Puede conectarse al tipo de conexión de Microsoft SQL Server o en el extremo de clúster de SQL Server datos de gran tamaño.
En Azure Data Studio, presione F1 y haga clic en **nueva conexión** y puede conectarse al punto de conexión de clúster de macrodatos de SQL Server.

![Image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>Examinar HDFS

Una vez conectado, podrá examinar la carpeta HDFS. SQL Server comienza WebHDFS se inicia cuando se completa la implementación. Con WebHDFS, puede **actualizar**, agregar **nuevo directorio**, **cargar** archivos, y **eliminar**.

![image2](media/notebooks-guidance/image2.png)

Estas operaciones simples permiten traer sus propios datos en HDFS.

## <a name="launch-new-notebooks"></a>Iniciar nuevos blocs de notas

>[!NOTE]
>Si tiene varios procesos de Python que se ejecuta en su entorno, primero elimine el `.scaleoutdata` carpeta bajo el directorio instalado. Esto debe desencadenar el `Reinstall Notebook dependencies` tareas en Azure Data Studio. Se tardará algunos minutos para todas las dependencias para instalarse.

Si hay problemas al instalar las dependencias del Bloc de notas, haga clic en Ctrl + Mayús + P o Macintosh Cmd + Mayús + P y el tipo `Reinstall Notebook dependencies` en la paleta de comandos.

![image3](media/notebooks-guidance/image3.png)

Hay varias formas de iniciar un nuevo cuaderno.

1. Desde el **administrar panel**. Después de realizar una nueva conexión, verá un panel. Haga clic en **nuevo cuaderno** tareas desde el panel.
  
    ![image4](media/notebooks-guidance/image4.png)

1. Haga clic en la conexión de Spark o HDFS y haga clic en **nuevo cuaderno** en el menú contextual.

    ![image5](media/notebooks-guidance/image5.png)

    Un nuevo archivo denominado `Notebook-0.ipynb` se abre.

    ![image6](media/notebooks-guidance/image6.png)

Cuando se abre el Bloc de notas desde la paleta de comandos, se abre el Bloc de notas como `Untitled-0.ipynb`.

## <a name="supported-kernels-and-attach-to-context"></a>Admite los kernels y asociar al contexto

La instalación de Bloc de notas es compatible con PySpark y Spark, los kernels de Sparkmagic, que le permiten escribir código de Python y Scala con Spark. Si lo desea, puede elegir Python para fines de desarrollo local.

![image7](media/notebooks-guidance/image7.png)

Cuando selecciona uno de estos kernels, la instalación configura esa kernel en el entorno virtual y puede empezar a escribir código en el idioma.

|Kernel|Descripción
|:-----|:-----
|PySpark3 y Kernel PySpark| Escribir código de Python mediante el proceso de Spark del clúster.
|Spark Kernel|Escribir código de Scala y R mediante el proceso de Spark del clúster.
|Python Kernel|Escribir código de Python para el desarrollo local.

`Attach to` proporciona el contexto para el Kernel adjuntar. Cuando esté conectado al punto de final de SQL Server macrodatos clúster, el valor predeterminado `Attach to` es ese punto de conexión del clúster.

Cuando no están conectados al punto final de clúster de SQL Server datos de gran tamaño, el Kernel predeterminado es Python y `Attach to` es `localhost`.

## <a name="hello-world-in-different-contexts"></a>Hello world en contextos diferentes

### <a name="pyspark3pyspark-kernel"></a>Kernel Pyspark3/PySpark

Elija el Kernel de PySpark y en el tipo de celda en el código siguiente.

Haga clic en **Ejecutar**.

La aplicación de Spark se inicia y devuelve el siguiente resultado:

![image8](media/notebooks-guidance/image8.png)

### <a name="spark-kernel--scala-language"></a>Kernel de Spark | Lenguaje de scala

Elija el Spark | scala Kernel y en el tipo de celda en el código siguiente.

![image9](media/notebooks-guidance/image9.png)

Agregar una nueva celda de código haciendo clic en el **+ código** comando en la barra de herramientas.

Ahora, elija el Spark | Scala en la lista desplegable de los kernels y en la celda escriba o pegue en:

![Image10](media/notebooks-guidance/image10.png)

También puede ver las opciones de"celda" al hacer clic en el icono de opciones siguiente:

![Image11](media/notebooks-guidance/image11.png)

### <a name="spark-kernel--r-language"></a>Kernel de Spark | Lenguaje R

Elija el Spark | R en la lista desplegable de los kernels. En la celda, escriba o pegue el código. Haga clic en **ejecutar** para ver el resultado siguiente.

![Image13](media/notebooks-guidance/image13.png)

### <a name="local-python-kernel"></a>Kernel de Python local

Elija el Kernel de Python local y en el tipo de celda:

![Image14](media/notebooks-guidance/image14.png)

### <a name="markdown-text"></a>Text v markdownu

Agregar una nueva celda de texto haciendo clic en el **+ texto** comando en la barra de herramientas.

![Image15](media/notebooks-guidance/image15.png)

Haga doble clic en cambiar para modificar la vista de la celda de texto 

![Image16](media/notebooks-guidance/image16.png)

La celda cambia al modo de edición

![Image17](media/notebooks-guidance/image17.png)

Ahora markdown de tipo y verá la vista previa a la vez

![Image18](media/notebooks-guidance/image18.png)

Haga clic en **Ejecutar**. Se inicia la aplicación de Spark se crea la sesión de Spark como **spark** y define la **HelloWorld** objeto.

El Bloc de notas debe ser similar a la siguiente imagen.

Hacer clic fuera de la celda de texto cambiará al modo de vista previa y oculta el marcado.

![Image19](media/notebooks-guidance/image19.png)


## <a name="manage-packages"></a>Administración de paquetes
Una de las cosas que hemos optimizado para el desarrollo de Python local era incluyen la capacidad para instalar los paquetes que los clientes tendrían para sus escenarios. De forma predeterminada, se incluyen los paquetes comunes como `pandas`, `numpy` etc., pero si se espera un paquete que no se incluye a continuación, escribir el código siguiente en la celda del Bloc de notas: 

```python
import <package-name>
```

Al ejecutar este comando, `Module not found` se devuelve. Si el paquete no existe, no obtendrá el error.

Si devuelve un `Module not Found` error y, a continuación, haga clic en **administrar paquetes** para iniciar el terminal con la ruta de acceso para su Virtualenv identificado. Ahora puede instalar los paquetes localmente. Use los siguientes comandos para instalar los paquetes:

```bash
./pip install <package-name>
```

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