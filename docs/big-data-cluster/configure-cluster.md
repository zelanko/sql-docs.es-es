---
title: Configuración del inicio de sesión del clúster
titleSuffix: Configure a SQL Server big data cluster
description: Introducción a la configuración de un clúster de macrodatos de SQL Server
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 08/04/2020
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b75f6946af9a13d6a8202c627d4c24a2225a51c1
ms.sourcegitcommit: 4545b502e3cae7136411fd9a7c15450315665f38
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2020
ms.locfileid: "94549997"
---
# <a name="configure-a-sql-server-big-data-cluster"></a>Configuración de un clúster de macrodatos de SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Puede configurar las propiedades de la instancia maestra de SQL Server, Apache Spark y Apache Hadoop en el clúster de macrodatos de SQL Server 2019 en el momento de la implementación.

Después de la implementación, los clústeres de macrodatos no admiten la modificación de las propiedades de configuración.

## <a name="configuration-scopes"></a>Ámbitos de configuración
La configuración de los Clústeres de macrodatos tiene dos niveles de ámbito: `service` y `resource`. La jerarquía de la configuración también sigue este orden, de mayor a menor. Los componentes de BDC tomarán el valor de la configuración que se define en el ámbito inferior. Si la configuración no se define en un ámbito determinado, heredará el valor de su ámbito principal superior.

Por ejemplo, puede que quiera definir el número predeterminado de núcleos que el controlador de Spark usará en el Bloque de almacenamiento y Sparkhead `resources`. Puede hacerlo de dos maneras: 
- Especifique un valor predeterminado de núcleos en el ámbito de servicio `Spark`  
- Especifique un valor predeterminado de núcleos en el ámbito de recursos `storage-0` y `sparkhead`

En el primer escenario, todos los recursos con ámbito inferior del servicio de Spark (Bloque de almacenamiento y Sparkhead) *heredarán* el número predeterminado de núcleos del valor predeterminado del servicio de Spark.

En el segundo escenario, cada recurso usará el valor definido en su ámbito respectivo.

Si el número predeterminado de núcleos se configura tanto en el ámbito de servicio como en el de ámbito, el valor con ámbito de recurso reemplazará el valor con ámbito de servicio, porque se trata del ámbito **configurado por el usuario** inferior para la configuración determinada.

Para obtener información específica sobre la configuración, vea los artículos siguientes:

Procedimientos: 
- [Configuración de una instancia maestra de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](configure-sql-server-master-instance.md)
- [Configuración de Apache Spark y Apache Hadoop en clústeres de macrodatos](configure-spark-hdfs.md)

Referencia: 
- [Propiedades de configuración de la instancia maestra de SQL Server](reference-config-master-instance.md)
- [Propiedades de configuración de Apache Spark y Apache Hadoop (HDFS)](reference-config-spark-hadoop.md)
