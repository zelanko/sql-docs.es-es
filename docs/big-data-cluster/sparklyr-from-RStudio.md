---
title: Usar sparklyr de RStudio
titleSuffix: SQL Server big data clusters
description: Conéctese al clúster de macrodatos con sparklyr de RStudio.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 30b8ddccd01c0e8d9a4eac34f2f504b0d8971af6
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860196"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>Usar Sparklyr en clúster de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr proporciona una interfaz de R para Apache Spark. Sparklyr es la forma de preferido para los desarrolladores de R usen Spark. Este artículo describe cómo usar sparklyr en un clúster de macrodatos de 2019 de SQL Server (versión preliminar) mediante RStudio.

## <a name="prerequisites"></a>Requisitos previos

- [Implementar un clúster de SQL Server 2019 macrodatos](quickstart-big-data-cluster-deploy.md).
- [Instalación de RStudio](https://www.rstudio.com/)

## <a name="connect-to-spark-in-ss19-big-data-cluster"></a>Conectarse a spark en clústeres SS19 Big Data

En RStudio crear un RScript y conéctese a la de Spark como sigue. Clúster de macrodatos de Spark se conecta a través de Livy, que puede ponerse en contacto con el [puerta de enlace de Spark o HDFS](connect-to-big-data-cluster.md#hdfs). Para la autenticación, utilice el nombre de usuario y contraseña que estableció durante la implementación.

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "***root***", password = "****")

httr::set_config(httr::config(ssl_verifypeer = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>Ejecutar consultas de sparklyr

Después de conectarse a Spark, puede ejecutar sparklyr. El ejemplo siguiente realiza una consulta en el conjunto de datos de iris mediante sparklyr:

``` r
copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de datos de gran tamaño, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos?](big-data-cluster-overview.md).