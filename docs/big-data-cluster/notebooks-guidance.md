---
title: Ejecutar blocs de notas en Azure Data Studio
titleSuffix: SQL Server 2019 big data clusters
description: Este artículo explica cómo ejecutar Jupyter Notebook en Azure Data Studio conneected a un clúster de macrodatos de SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: af1393b38b297e451903d5a39942a3e878c88ee6
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53246614"
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

## <a name="connect-to-the-hadoop-gateway-knox-end-point"></a>Conectar con el punto final de Knox de puerta de enlace de Hadoop

Puede conectarse a diferentes puntos de conexión del clúster. Puede conectarse al tipo de conexión de Microsoft SQL Server o en el extremo de la puerta de enlace de Spark o HDFS.
En Azure Data Studio (versión preliminar), presione F1 y haga clic en **nueva conexión** y puede conectarse al punto de conexión de puerta de enlace de Spark o HDFS.

![Image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>Examinar HDFS

Una vez conectado, podrá examinar la carpeta HDFS. WebHDFS se inicia cuando se completa la implementación y podrán realizar **actualizar**, agregar **nuevo directorio**, **cargar** archivos, y **eliminar**.

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

  Proporcione un nombre de su portátil, por ejemplo, `Test.ipynb`. Haga clic en **Guardar**.

![image6](media/notebooks-guidance/image6.png)

## <a name="supported-kernels-and-attach-to-context"></a>Admite los kernels y asociar al contexto

La instalación de Bloc de notas es compatible con PySpark y Spark, los kernels de Sparkmagic, que le permiten escribir código de Python y Scala con Spark. Si lo desea, puede elegir Python para fines de desarrollo local.

![image7](media/notebooks-guidance/image7.png)

Cuando selecciona uno de estos kernels, instalaremos esa kernel en el entorno virtual y puede empezar a escribir código en el idioma.

|Kernel|Descripción
|:-----|:-----
|Kernel de PySpark|Para escribir código de Python mediante el proceso de Spark del clúster.
|Kernel de Spark|Para escribir código Scala mediante el proceso de Spark del clúster.
|Kernel de Python|Para escribir código de Python para el desarrollo local.

El `Attach to` proporciona el contexto para el Kernel adjuntar. Cuando se conecta al final de la puerta de enlace (Knox) Spark o HDFS, seleccione el valor predeterminado `Attach to` es ese punto de conexión del clúster.

![image8](media/notebooks-guidance/image8.png)

## <a name="hello-world-in-different-contexts"></a>Hello world en contextos diferentes

### <a name="pyspark-kernel"></a>Kernel de Pyspark

Elija el Kernel de PySpark y en el tipo de celda en el código siguiente:

![image9](media/notebooks-guidance/image9.png)

Haga clic en ejecutar y se debe ver la aplicación de Spark que se está iniciando y verá el siguiente resultado:

![Image10](media/notebooks-guidance/image10.png)

La salida debe tener un aspecto similar a la siguiente imagen.

![Image11](media/notebooks-guidance/image11.png)

### <a name="spark-kernel"></a>Kernel de Spark
Agregar una nueva celda de código haciendo clic en el **+ código** comando en la barra de herramientas.

![Image12](media/notebooks-guidance/image12.png)

También puede ver las opciones de"celda" al hacer clic en el icono de opciones siguiente:

![Image13](media/notebooks-guidance/image13.png)

Estas son las opciones para cada celda:

![Image14](media/notebooks-guidance/image14.png)-

Ahora, elija el Kernel de Spark en la lista desplegable de los kernels y en la celda escriba o pegue en:

![Image15](media/notebooks-guidance/image15.png)

Haga clic en **ejecutar** y debería ver la aplicación de Spark que se está iniciando y se creará la sesión de Spark como **spark** y definirá el **HelloWorld** objeto.

El Bloc de notas debe ser similar a la siguiente imagen.

![Image16](media/notebooks-guidance/image16.png)

Una vez que defina el objeto, a continuación, en la siguiente celda del Bloc de notas, escriba en el código siguiente:

![Image17](media/notebooks-guidance/image17.png)

Haga clic en **ejecutar** en el Bloc de notas y menú verá el "Hello, world!" en la salida.

![Image18](media/notebooks-guidance/image18.png)

### <a name="local-python-kernel"></a>Kernel de python local
Elija el Kernel de Python local y en el tipo de celda:

![Image19](media/notebooks-guidance/image19.png)

Verá lo siguiente:

![Image20](media/notebooks-guidance/image20.png)

### <a name="markdown-text"></a>Text v markdownu
Agregar una nueva celda de texto haciendo clic en el **+ texto** comando en la barra de herramientas.

![Image21](media/notebooks-guidance/image21.png)

Haga clic en el icono de vista previa para agregar el código de markdown

![Image22](media/notebooks-guidance/image22.png)

Haga clic en el icono de vista previa nuevo para alternar para ver el código de markdown

![Image23](media/notebooks-guidance/image23.png)

## <a name="manage-packages"></a>Administración de paquetes
Una de las cosas que hemos optimizado para el desarrollo de Python local era incluyen la capacidad para instalar los paquetes que los clientes tendrían para sus escenarios. De forma predeterminada, se incluyen los paquetes comunes, como pandas, numpy, etc., pero si se espera que un paquete que no se incluye a continuación, escribir el código siguiente en la celda del Bloc de notas: 

```python
import <package-name>
```

Al ejecutar este comando, obtendrá un `Module not found` error. Si el paquete no existe, no obtendrá el error.

Si encuentra un `Module not Found` error y, a continuación, haga clic en **administrar paquetes** para iniciar el terminal con la ruta de acceso para su Virtualenv identificado. Ahora puede instalar los paquetes localmente. Use los siguientes comandos para instalar los paquetes:

```bash
./pip install <package-name>
```

Después de instalar el paquete, debe ir en la celda del Bloc de notas y escriba en el siguiente comando:

```python
import <package-name>
```

Ahora al ejecutar la celda, ya no se debe obtener el `Module not found` error.

Para desinstalar un paquete, use el siguiente comando desde el terminal:

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre cómo trabajar con un bloc de notas existente, consulte [cómo administrar los cuadernos en Azure Data Studio](notebooks-how-to-manage.md).