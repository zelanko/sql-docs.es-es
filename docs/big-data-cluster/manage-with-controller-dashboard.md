---
title: Administración de SQL Server clúster de macrodatos con el panel del controlador
titleSuffix: Manage SQL Server big data cluster with controller dashboard
description: Use un cuaderno de Azure Data Studio para administrar un clúster de macrodatos y solucionar problemas de este.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 08/29/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5fadb9b069e6f70cb780e6dc69295f63330a683a
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160718"
---
# <a name="manage-big-data-clusters-for-sql-server-controller-dashboard"></a>Administración de clústeres de macrodatos para el panel de SQL Server Controller

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Además de **azdata** y el cuaderno de estado del clúster, hay otra manera de ver el estado de un clúster de macrodatos SQL Server. Ahora puede Agregar el controlador de clúster del SQL Server Big Data a través de las **conexiones** Viewlet. Esto le permite tener un panel para ver el estado del clúster.

![dashboard](media/manage-with-controller-dashboard/controller-dashboard.png)
## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para iniciar el cuaderno:

* Versión más reciente de la [compilación Azure Data Studio Insiders](https://docs.microsoft.com/sql/big-data-cluster/deploy-big-data-tools?view=sqlallproducts-download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc)
* Extensión [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] instalada en Azure Data Studio

Además de lo anterior, SQL Server clúster de macrodatos de 2019 también requiere:

* **azdata**
    - [Administrador de paquetes de Linux](deploy-install-azdata-linux-package.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI de Azure](/cli/azure/install-azure-cli)


## <a name="add-sql-server-big-data-cluster-controller"></a>Agregar SQL Server controlador de clúster de Big Data

1. Haga clic en la vista conexiones en el panel izquierdo.
2. En la parte inferior de la vista conexiones, haga clic en **SQL Server clústeres de Big Data** para expandirlo.
3. Haga clic en **agregar SQL Server controlador de clúster de Big Data**; se abrirá un nuevo cuadro de diálogo.

## <a name="add-new-controller"></a>Agregar nuevo controlador

1. Agregue el nombre del clúster.
2. Agregue la dirección URL del servicio de administración de clústeres. Esto se puede encontrar en la tabla de puntos de conexión de servicio en el panel de BDC o en el administrador de clústeres.
3. Agregue su nombre de usuario y contraseña.

## <a name="launch-controller-dashboard"></a>Panel de inicio del controlador

1. Cuando agregue correctamente el controlador, puede verlo en SQL Server clústeres de macrodatos.
2. Para iniciar el panel, haga clic con el botón derecho en el controlador y haga clic en **administrar**.

## <a name="controller-dashboard"></a>Panel del controlador

1. En el panel del controlador, hay 3 componentes principales:

    - **Barra de herramientas** en la parte superior que contiene acciones para el panel.
    - **Panel de navegación** a la izquierda que cambia a las distintas vistas en el panel.
    - **Vista** que abarca la mayoría de la página.

2. En la página de **información general del clúster de Big Data** , puede ver:

    - **Propiedades de clúster** para ver información sobre el clúster.
    - **Información general del clúster** para ver información general de alto nivel sobre todos los componentes del clúster y cuáles son incorrectos
    - **Puntos de conexión de servicio** para copiar o tener acceso a diferentes servicios dentro del clúster de macrodatos de SQL Server.

3. En el **Panel de navegación,** puede ver la lista de servicios y hacer clic en uno para ver detalles adicionales del clúster. Se trata de las mismas vistas al hacer clic en un servicio en **información general del clúster.**

4. Cada vista en **detalles del clúster** consta de los mismos componentes de la interfaz de usuario:

    - **Detalles de estado de mantenimiento** que comparten el estado y el estado de mantenimiento del componente.
    - **Métricas y registros** para ver métricas y registros adicionales a través de Grafana y Kibana.

1. Si ve un componente que está en mal estado, haga clic en **solucionar problemas** en la barra de herramientas para iniciar un libro de Jupyter que contenga un cuaderno que le ayude a diagnosticar el problema.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el controlador, consulte [nuestra documentación del controlador](concept-controller.md).