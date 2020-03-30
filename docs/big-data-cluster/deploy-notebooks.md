---
title: 'Implementación: cuadernos de Azure Data Studio'
titleSuffix: SQL Server Big Data Clusters
description: Use un cuaderno de Azure Data Studio para implementar un clúster de macrodatos.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e11a4ac0bcbb66d6b3216d8c2f7a4a3b15cedfb8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75246868"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebook"></a>Implementación de clústeres de macrodatos de SQL Server con un cuaderno de Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] proporciona una extensión para Azure Data Studio que incluye cuadernos de implementación. Un cuaderno de implementación incluye documentación y código que se puede usar en Azure Data Studio para crear un clúster de macrodatos de SQL Server.

Los [cuadernos](notebooks-guidance.md), que al principio se implementaban como un proyecto de código abierto, se han implementado en [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download). Puede usar Markdown para el texto de las celdas de texto y uno de los kernels disponibles para escribir código en las celdas de código.

Puede usar cuadernos para implementar clústeres de macrodatos para [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

## <a name="prerequisites"></a>Prerrequisitos

Los siguientes requisitos previos son indispensables para iniciar también el cuaderno:

* Versión más reciente de la [compilación Azure Data Studio Insiders](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master) instalada

Además de lo anterior, la implementación de clústeres de macrodatos de SQL Server 2019 también requiere:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI de Azure (si se implementa en Azure)](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)

## <a name="launch-the-notebook"></a>Inicio del cuaderno

1. Inicie Azure Data Studio.

2. En la pestaña **Conexiones**, seleccione los puntos suspensivos ( **...** ) y, a continuación, seleccione **Implementar SQL Server...** .

   ![Implementar SQL Server](media/deploy-notebooks/deploy-notebooks.png)

3. En las opciones de implementación, seleccione **Clúster de macrodatos de SQL Server**.

4. En **Deployment Target** (Destino de implementación), en **Opciones**, seleccione **New Azure Kubernetes Cluster** (Nuevo clúster de Azure Kubernetes) o **Existing Azure Kubernetes Service cluster** (Clúster de Azure Kubernetes Service existente).

5. Acepte los términos de privacidad y de licencia.

6. En este cuadro de diálogo también se comprueba si en el host están las herramientas necesarias para el tipo seleccionado de implementación de SQL. El botón **Seleccionar** no se habilita hasta que se haya efectuado correctamente la comprobación de las herramientas.

7. Seleccione el botón **Seleccionar**. Esta acción inicia la experiencia de implementación.

## <a name="set-deployment-configuration-template"></a>Establecer una plantilla de configuración de implementación

Puede personalizar la configuración del perfil de implementación siguiendo las instrucciones que se indican a continuación.

### <a name="target-configuration-template"></a>Plantilla de configuración de destino

Seleccione la plantilla de configuración de destino en las plantillas disponibles. Los perfiles disponibles se filtran según el tipo de destino de implementación que se elija en el cuadro de diálogo anterior.

   ![Paso 1 de la plantilla de configuración de implementación](media/deploy-notebooks/deployment-configuration-template.png)

### <a name="azure-settings"></a>Configuración de azure

Si el destino de implementación es un AKS nuevo, se necesitará información adicional, como el identificador de suscripción de Azure, el grupo de recursos, el nombre del clúster de AKS, el recuento de VM, el tamaño y demás información adicional para crear el clúster de AKS.

   ![Configuración de azure](media/deploy-notebooks/azure-settings.png)

Si el destino de implementación es un clúster de Kubernetes existente, el asistente solicitará la ruta de acceso al archivo de configuración *kube* para importar las opciones de configuración de clúster de Kubernetes. Asegúrese de que esté seleccionado el contexto de clúster adecuado en el que se puede implementar el Clúster de macrodatos de SQL Server 2019.

   ![Contexto del clúster de destino](media/deploy-notebooks/target-cluster-context.png)

### <a name="cluster-docker-and-ad-settings"></a>Configuración de clúster, Docker y AD

1. Escriba el nombre del clúster para el BDC de SQL Server 2019, el nombre de usuario de administrador y la contraseña.
Nota: Se usa la misma cuenta para el controlador y para SQL Server.

   ![Configuración de clúster](media/deploy-notebooks/cluster-settings.png)

2. Escriba la configuración de Docker según corresponda.

   ![Configuración de Docker](media/deploy-notebooks/docker-settings.png)

3. Si la autenticación de AD está disponible, escriba la configuración de AD.

   ![Configuración de Active Directory](media/deploy-notebooks/active-directory-settings.png)

### <a name="service-settings"></a>Configuración del servicio

Esta pantalla contiene entradas para diversas opciones, como **Escala**, **Puntos de conexión**, **Almacenamiento** y otras **opciones de almacenamiento avanzadas**. Escriba los valores adecuados y seleccione **Siguiente**.

#### <a name="scale-settings"></a>Configuración de escala

Escriba el número de instancias de cada uno de los componentes del clúster de macrodatos.

Se puede incluir una instancia de Spark junto con HDFS. Se incluye en el grupo de almacenamiento o por sí misma en el grupo de Spark.

   ![Configuración del servicio](media/deploy-notebooks/service-settings.png)

Para obtener más información sobre cada uno de estos componentes, puede consultar [instancia maestra](concept-master-instance.md), [grupo de datos](concept-data-pool.md), [grupo de almacenamiento](concept-storage-pool.md) o [grupo de proceso](concept-compute-pool.md).

#### <a name="endpoint-settings"></a>Configuración de punto de conexión

Los puntos de conexión predeterminados se han rellenado previamente. Sin embargo, se pueden cambiar según corresponda.

   ![Configuración de punto de conexión](media/deploy-notebooks/endpoint-settings.png)

#### <a name="storage-settings"></a>Configuración de almacenamiento

La configuración de almacenamiento incluye la clase de almacenamiento y el tamaño de las notificaciones para los datos y los registros. La configuración se puede aplicar en el grupo de almacenamiento, de datos y el maestro de SQL Server.

   ![Configuración de almacenamiento](media/deploy-notebooks/storage-settings.png)

#### <a name="advanced-storage-settings"></a>Configuración de almacenamiento avanzada

Puede agregar más opciones de configuración de almacenamiento en **Configuración avanzada de almacenamiento**.

* Grupo de almacenamiento (HDFS)
* Grupo de datos
* Maestro de SQL Server

   ![Configuración de almacenamiento avanzada](media/deploy-notebooks/advanced-storage-settings.png)

### <a name="summary"></a>Resumen

Esta pantalla resume toda la entrada proporcionada para implementar el clúster de macrodatos de SQL Server 2019. Los archivos de configuración se pueden descargar con el botón **Guardar archivos de configuración**. Seleccione **Script en cuaderno** para incluir toda la configuración de implementación en un script de un cuaderno. Una vez abierto el cuaderno, seleccione **Ejecutar celdas** para iniciar la implementación del BDC de SQL Server 2019 en el destino seleccionado.

   ![Resumen](media/deploy-notebooks/deploy-sql-server-big-data-cluster-on-a-new-AKS-cluster.png)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la implementación, consulte la [guía de implementación para los clústeres de macrodatos de SQL Server](deployment-guidance.md).
