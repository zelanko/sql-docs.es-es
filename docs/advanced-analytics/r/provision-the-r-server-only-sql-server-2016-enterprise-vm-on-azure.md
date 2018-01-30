---
title: "Aprovisionar una máquina virtual para el aprendizaje automático de Azure | Documentos de Microsoft"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 781622d51b7112d3a501652b7c320ab27e74ae35
ms.sourcegitcommit: c77a8ac1ab372927c09bf241d486e96881b61ac9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2018
---
# <a name="provision-a-virtual-machine-for-machine-learning-on-azure"></a>Aprovisionar una máquina virtual para el aprendizaje automático de Azure

Máquinas virtuales en Azure son una opción adecuada para configurar rápidamente un entorno de servidor completa para las soluciones de aprendizaje automático.

Este artículo enumeran las imágenes de máquina virtual que contienen SQL Server con aprendizaje automático, así como algunas máquinas virtuales relacionadas.

En este artículo también proporciona respuestas a preguntas habituales sobre cómo modificar o actualizar una instancia existente de SQL Server en una máquina virtual.

+ [Lista de máquinas virtuales actuales](#bkmk_list)

## <a name="provision-a-virtual-machine-with-sql-server-and-machine-learning"></a>Aprovisionar una máquina virtual con SQL Server y aprendizaje automático

Si está familiarizado con el uso de máquinas virtuales de Azure, se recomienda que consulte los siguientes artículos para obtener más información sobre cómo usar el portal y configurar una máquina virtual.

+ [Máquinas virtuales: introducción](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [Primeros pasos con máquinas virtuales de Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/)

Asegúrese de usar la nueva versión del portal de Azure o Azure Marketplace. Algunas imágenes no están disponibles al examinar la Galería de Azure en el portal clásico.

**Crear la máquina virtual**

1. Abra el portal de Azure: [portal.azure.com](https:portal.azure.com).

2. Haga clic en **máquinas virtuales**, o haga clic en **nuevo**.

3. Haga clic en **Agregar**.

4. En el cuadro de búsqueda en la parte superior de la página, escriba "Servidor de aprendizaje de máquina" o "SQL Server" para ver una lista de máquinas virtuales relacionadas.

5. Revise los requisitos y haga clic en **crear** para empezar a trabajar.

6. Después de la máquina virtual se ha creado y se está ejecutando, haga clic en el **conectar** botón para abrir una conexión e iniciar sesión en la nueva máquina.

5. Después de conectarse, puede instalar paquetes de R o Python adicionales o configure la herramienta de desarrollo preferido.

### <a name="connect-to-the-virtual-machine"></a>Conéctese a la máquina virtual.

La manera en que un cliente se conecta a SQL Server que se ejecuta en una máquina virtual varía según la ubicación del cliente y la configuración de red.

Para obtener más información, consulte [conectar a una máquina virtual de SQL Server en Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-connect).

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

Esta sección contiene algunas preguntas comunes sobre máquinas virtuales de Microsoft de aprendizaje automático.

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>¿Se puede instalar una máquina virtual con SQL Server 2017?

Una máquina de virtual basada en Windows para SQL Server de 2017 Enterprise Edition que incluye servicios de aprendizaje de máquina está disponible a partir de noviembre de 2017. 

Para los anuncios sobre nuevas máquinas virtuales de ciencia de datos, supervisar estos sitios de blog:

+ [Inteligencia de Cortana y el aprendizaje automático](https://blogs.technet.microsoft.com/machinelearning/)
+ [Iniciados de la plataforma de datos](https://blogs.technet.microsoft.com/dataplatforminsider/)

### <a name="adding-sql-server-to-an-existing-virtual-machine"></a>Agregar SQL Server a una máquina virtual existente

Además de crear una máquina virtual con una imagen que ya incluye SQL Server aprendizaje automático, puede instalar a SQL Server en una máquina virtual existente y habilitar el características de aprendizaje automático. Se recomienda la edición Enterprise o Developer, para evitar las restricciones de recursos. La instalación también requiere que use su propia clave de licencia.

Al ejecutar el programa de instalación, asegúrese de seleccionar la característica y al menos un idioma (R o Python) de aprendizaje de automático. Algunos pasos adicionales son necesarios para habilitar los servicios de aprendizaje de máquina para comunicarse con SQL Server y para activar la red en la máquina virtual.

Para obtener más información, consulte [Installing SQL Server R Services en una máquina virtual de Azure](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md).

### <a name="using-machine-learning-in-azure-sql-database"></a>Usar aprendizaje automático en base de datos SQL de Azure

Actualmente, la vista previa de soporte técnico de R en SQL Azure está suspendida por el trabajo de desarrollo en curso. Para obtener más información, consulte [base de datos de SQL Azure](../r/using-r-in-azure-sql-database.md).

### <a name="can-i-upgrade-the-sql-server-version-on-a-virtual-machine"></a>¿Se puede actualizar la versión de SQL Server en una máquina virtual?

Aunque las imágenes de SQL Server 2016 admiten R, si desea utilizar Python, puede actualizar a SQL Server 2017, que también actualiza los otro componentes de aprendizaje automático.

Para actualizar la versión de SQL Server que está instalado, abra el centro de instalación de SQL Server en la máquina virtual y seleccione el **actualizar** opción. Dependiendo de la máquina virtual que ha creado, una licencia podría requerirse.

Para obtener más información, consulte [actualizar SQL Server mediante el Asistente para la instalación](https://docs.microsoft.com/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup).

### <a name="can-i-upgrade-just-the-machine-learning-components"></a>¿Puedo actualizar solo los componentes de aprendizaje de automático?

Cuando se publican nuevas actualizaciones para RevoScaleR, MicrosoftML o revoscalepy, puede actualizar los componentes utilizados por SQL Server, mediante el uso de un proceso conocido como de aprendizaje automático _enlace_. Esto no cambia la versión de SQL Server, pero cambiar la directiva de soporte técnico para la instancia.

Para obtener más información, consulte [SqlBindR de uso para actualizar los componentes de aprendizaje de máquina en SQL Server](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>¿Cómo se tiene acceso a los datos de una cuenta de almacenamiento de Azure?

Cuando tenga que usar los datos de su cuenta de almacenamiento de Azure, habrá varias opciones para obtener acceso a los datos o moverlos:

+ Copie los datos de la cuenta de almacenamiento al sistema de archivos local con una utilidad, como [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only). 

+ Agregue los archivos a un recurso compartido de archivos en la cuenta de almacenamiento y, luego, monte el recurso compartido de archivos como una unidad de red en la máquina virtual. Para más información, consulte [Montaje de archivos de Azure](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/). 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>¿Cómo se usan los datos de una cuenta de Azure Data Lake Storage (ADLS)?

Puede leer datos desde el almacenamiento ADLS con RevoScaleR, mediante el uso de webHDFS para hacer referencia a la cuenta de almacenamiento de sistema de archivos de la misma manera que lo haría con un HDFS. Para obtener más información, consulte este artículo: [usar R para realizar operaciones de sistema de archivos en el almacén de Azure Data Lake](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/).

### <a name="i-cant-find-the-rre-virtual-machine"></a>No se encuentra la máquina virtual RRE

El "RRE para la máquina Virtual de Windows" que estaba disponible anteriormente en Azure Marketplace se ha reemplazado por la imagen de "Machine Learning Server para Windows".

Imágenes de servidor de aprendizaje de máquina también están disponibles para la versión de CentOS Linux 7.2, versión de Linux RedHat 7.2 y Ubuntu versión 16.04.

Para obtener más información, vea [servidor de aprendizaje de máquina en la nube](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-in-the-cloud)

### <a name="configuring-machine-learning-server-or-r-server-to-support-web-services"></a>Configurar servidor de aprendizaje de máquina o un servidor de R para admitir los servicios web

Si usa una máquina virtual que incluye el servidor de aprendizaje de máquina, una configuración adicional podría ser necesaria para usar la implementación del servicio web, ejecución remota, o para usar la máquina virtual como un servidor de implementación en su organización.

Para obtener instrucciones, consulte [configuración del servidor de aprendizaje máquina para hacer operativos los análisis](https://docs.microsoft.com/machine-learning-server/operationalize/configure-machine-learning-server-one-box).

No se necesita configuración adicional si desea utilizar paquetes como RevoScaleR o MicrosoftML.

## <a name="bkmk_list"></a>Lista de máquinas virtuales

Actualmente, las siguientes máquinas virtuales están disponibles para el aprendizaje automático con SQL Server:

|Nombre| Comentarios|
|----|----|----|
| **SQL Server 2016**| ***  |
|SQL Server 2016 SP1 Enterprise en Windows|Servicios de R para análisis avanzado integrado.|
|BYOL SQL Server 2016 SP1 Enterprise en Windows Server |Servicios de R para análisis avanzado integrado. |
|Licencia gratuita: Programador SQL Server 2016 SP1 en Windows Server 2016 |Servicios de R para análisis avanzado integrado. |
| Data Science Virtual Machine - 2012 de Windows|Contiene herramientas populares de ciencia de datos, incluidos Microsoft R Server Developer Edition, SQL Server 2016 Developer edition, la distribución de Anaconda Python, edición para programadores de Julia Pro y Jupyter blocs de notas para R.| 
| Data Science Virtual Machine - 2016 de Windows|Incluye SQL Server 2016 Developer Edition, con compatibilidad para el análisis de R en bases de datos.|
|**SQL Server 2017**| ***   |
|SQL Server 2017 Enterprise Windows Server 2016| Servicios de aprendizaje de máquina con el soporte de lenguaje Python y R.|
|BYOL SQL Server 2017 Enterprise Windows Server 2016|Servicios de aprendizaje de máquina con el soporte de lenguaje Python y R.|
| Licencia de gratuito de SQL Server: Programador SQL Server 2017 en Windows Server|Servicios de aprendizaje de máquina con el soporte de lenguaje Python y R.|
| **Otro**| *** |
| Servidor solo SQL Server 2017 Enterprise de aprendizaje automático|Es similar a la imagen de SQL Server 2016 Enterprise, pero que contiene la versión independiente del servidor de aprendizaje de máquina y tiene el núcleo de ScaleR y funcionalidad de puesta en marcha optimizado para Windows entornos.|
| Aprendizaje automático de servidor para Windows|Contiene la versión independiente del servidor de aprendizaje de máquina, con características de puesta en marcha optimizados para entornos de Windows.|
|Máquina Virtual de ciencia de datos |Las ediciones de Linux son R Server. Máquinas virtuales de Linux que incluyen 2017 de SQL Server no se puede ejecutar código R o Python en SQL Server. Sin embargo, puede realizar en un modelo entrenado con la función de PREDICCIÓN de T-SQL de puntuación. Para obtener más información, consulte [puntuación nativo de SQl Server](../sql-native-scoring.md).|
