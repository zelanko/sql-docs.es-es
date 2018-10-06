---
title: Uso de cuadernos en versión preliminar de SQL Server 2019 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/05/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 989ee419406d0f69cd7bda26485d3d44cbf56550
ms.sourcegitcommit: c7d3a903eb7f410db3a0230101d24de0af17621a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2018
ms.locfileid: "48827336"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>Uso de cuadernos en versión preliminar de SQL Server 2019

Este artículo muestra cómo iniciar blocs de notas en un clúster de macrodatos de SQL Server 2019. También se muestra cómo empezar a crear sus propios cuadernos y cómo enviar trabajos en el clúster.

## <a name="prerequisites"></a>Requisitos previos

Para usar los blocs de notas, debe instalar los requisitos previos siguientes:

- [Un clúster de macrodatos de SQL Server 2019](deployment-guidance.md)
- [Studio datos de Azure](../azure-data-studio/what-is.md)
- [La extensión de SQL Server 2019 (versión preliminar)](../azure-data-studio/sql-server-2019-extension.md).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-sql-server-big-data-cluster-end-point"></a>Conectar con el punto de conexión del clúster de macrodatos de SQL Server

Puede conectarse a diferentes puntos de conexión del clúster. Puede conectarse al tipo de conexión de Microsoft SQL Server o para el punto de conexión del clúster de macrodatos de SQL Server.

En Azure Data Studio (versión preliminar), escriba **F1** > **nueva conexión**y conéctese a su punto de conexión del clúster de macrodatos de SQL Server.

![Image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>Examinar HDFS
Una vez conectado, podrá examinar la carpeta HDFS. WebHDFS se inicia cuando se completa la implementación y podrán realizar **actualizar**, agregar **nuevo directorio**, **cargar** archivos, y **eliminar**.

![image2](media/notebooks-guidance/image2.png)

Estas operaciones simples permiten traer sus propios datos en HDFS.

## <a name="launch-new-notebooks"></a>Iniciar nuevos blocs de notas

Hay varias formas de iniciar un nuevo cuaderno.

1. Desde el panel de administración. Acerca de cómo realizar una nueva conexión, verá un panel. Haga clic en la tarea de nuevo bloc de notas desde el panel.

  ![image3](media/notebooks-guidance/image3.png)

1. Haga clic con el botón derecho en la conexión de Spark o HDFS y tendrá un nuevo cuaderno en el menú contextual

![image4](media/notebooks-guidance/image4.png)

Proporcione un nombre del Bloc de notas (ejemplo: *Test.ipynb*) y haga clic en **guardar**.

![image5](media/notebooks-guidance/image5.png)

## <a name="supported-kernels-and-attach-to-context"></a>Admite los kernels y asociar al contexto

En nuestra instalación Bloc de notas, admitimos PySpark y Spark, los kernels de Sparkmagic que permiten a los usuarios escribir código de Python y Scala con Spark. También nos permiten a los usuarios elegir Python para sus fines de desarrollo local.

![image6](media/notebooks-guidance/image6.png)

Cuando selecciona uno de estos kernels, instalaremos esa kernel en el entorno virtual y puede empezar a escribir código en el idioma.

| Kernel | Descripción
|---- |----
|Kernel de PySpark| Para escribir código de Python con Spark, proceso del clúster.
|Kernel de Spark|Para escribir código Scala con Spark, proceso del clúster.
|Kernel de Python|Para escribir código de Python para el desarrollo local.

La selección para adjuntar proporciona el contexto para el Kernel adjuntar. Cuando se conectan para el punto de conexión del clúster de macrodatos de SQL Server, la selección predeterminada para adjuntar será ese punto de conexión del clúster.

![image7](media/notebooks-guidance/image7.png)

## <a name="hello-world-in-the-different-contexts"></a>Hola a todos en los contextos diferentes

### <a name="pyspark-kernel"></a>Kernel de Pyspark

Elija el Kernel de PySpark y en el tipo de celda en el código siguiente:

![image8](media/notebooks-guidance/image8.png)

Haga clic en ejecutar y se debe ver la aplicación de Spark que se está iniciando y verá el siguiente resultado:

![image9](media/notebooks-guidance/image9.png)

La salida debe tener un aspecto similar a la siguiente imagen.

![Image10](media/notebooks-guidance/image10.png)

### <a name="spark-kernel"></a>Kernel de Spark
Agregar una nueva celda de código haciendo clic en el + comando en la barra de herramientas de código.

![Image11](media/notebooks-guidance/image11.png)

Elija el Kernel de Spark en la lista desplegable para los kernels y en el tipo de celda y pegar en 

![Image12](media/notebooks-guidance/image12.png)

Haga clic en **ejecutar** debería ver la aplicación de Spark que se está iniciando y se creará la sesión de Spark **spark** y definirá el **HelloWorld** objeto.

El Bloc de notas debe ser similar a la siguiente imagen.

![Image13](media/notebooks-guidance/image13.png)

Una vez que se define el objeto, a continuación, en el siguiente tipo de celda del Bloc de notas en el código siguiente:

![Image14](media/notebooks-guidance/image14.png)

Haga clic en **ejecutar** en el Bloc de notas y menú verá el "Hello, world!" en la salida.

![Image15](media/notebooks-guidance/image15.png)

### <a name="local-python-kernel"></a>Kernel de python local
Elija el Kernel de Python local y en el tipo de celda en **

![Image16](media/notebooks-guidance/image16.png)

Verá lo siguiente:

![Image17](media/notebooks-guidance/image17.png)

### <a name="markdown-text"></a>Text v markdownu
Agregar una nueva celda de texto haciendo clic en el + comando de texto en la barra de herramientas.

![Image18](media/notebooks-guidance/image18.png)

Haga clic en el icono de vista previa para agregar el código de markdown

![Image19](media/notebooks-guidance/image19.png)

Haga clic en el icono de vista previa nuevo para alternar para ver el código de markdown

![Image20](media/notebooks-guidance/image20.png)

## <a name="manage-packages"></a>Administración de paquetes
Una de las cosas que hemos optimizado para el desarrollo de Python local era incluyen la capacidad para instalar los paquetes que los clientes tendrían para sus escenarios. De forma predeterminada, se incluyen los paquetes comunes, como pandas, numpy, etc., pero si se espera que un paquete que no se incluye a continuación, escribir el código siguiente en la celda del Bloc de notas

```python
import <package-name>
```

Al ejecutar este comando, obtendrá un `Module not found` error. Si el paquete no existe, no obtendrá el error.

Si encuentra un `Module not Found` error y, a continuación, haga clic en el **administrar paquetes** para iniciar el terminal con la ruta de acceso para su Virtualenv identificado. Ahora puede instalar los paquetes localmente. Use el siguiente comando para instalar los paquetes:

```
./pip install <package-name>
```

Después de instalar el paquete, debe ir en la celda del Bloc de notas y escriba el comando siguiente:

```python
import <package-name>
```

Ahora al ejecutar la celda, ya no se debe obtener el `Module not found` error.

Si desea desinstalar un paquete, use el siguiente comando desde el terminal:

```
./pip uninstall <package-name>
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre cómo trabajar con un bloc de notas existente, consulte [cómo administrar los cuadernos en Azure Data Studio](notebooks-how-to-manage.md).