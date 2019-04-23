---
title: Usar sparklyr de RStudio
titleSuffix: SQL Server big data clusters
description: Conéctese al clúster de macrodatos con sparklyr de RStudio.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 04/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 148e4942babafb35af2efe33eb427f9462f0a47e
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59969881"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>Usar sparklyr en clúster de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr proporciona una interfaz de R para Apache Spark. Sparklyr es una forma popular para los desarrolladores de R usen Spark. Este artículo describe cómo usar sparklyr en un clúster de macrodatos de 2019 de SQL Server (versión preliminar) mediante RStudio.

## <a name="prerequisites"></a>Requisitos previos

- [Implementar un clúster de SQL Server 2019 macrodatos](quickstart-big-data-cluster-deploy.md).

### <a name="install-rstudio-desktop"></a>Instalar RStudio Desktop

Instalar y configurar **RStudio Desktop** con los pasos siguientes:

1. Si está ejecutando en un cliente de Windows, [descargar e instalar R 3.4.4](https://cran.rstudio.com/bin/windows/base/old/3.4.4).

1. [Descargar e instalar RStudio Desktop](https://www.rstudio.com/products/rstudio/download/).

1. Una vez finalizada la instalación, ejecute los siguientes comandos dentro de RStudio Desktop para instalar los paquetes necesarios:

   ```RStudio Desktop install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01") install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01") install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## Connect to Spark in a big data cluster

You can use sparklyr to connect from a client to the big data cluster using Livy and the HDFS/Spark gateway. 

In RStudio, create an R script and connect to Spark as in the following example:

> [!TIP]
> For the `<USERNAME>` and `<PASSWORD>` values, use the username (such as root) and password you set during the big data cluster deployment. For the `<IP>` and `<PORT>` values, see the documentation on the [HDFS/Spark gateway](connect-to-big-data-cluster.md#hdfs).

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "<username>", password = "<password>")

httr::set_config(httr::config(ssl_verifypeer = 0L, ssl_verifyhost = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>Ejecutar consultas de sparklyr

Después de conectarse a Spark, puede ejecutar sparklyr. El ejemplo siguiente realiza una consulta en el conjunto de datos de iris mediante sparklyr:

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>Cálculos de R distribuidos

Una característica de sparklyr es la capacidad de [distribuyen los cálculos de R](https://spark.rstudio.com/guides/distributed-r/) con [spark_apply](https://spark.rstudio.com/reference/spark_apply/).

Dado que los clústeres de datos de gran tamaño usan conexiones de Livy, debe establecer `packages = FALSE` en la llamada a **spark_apply**. Para obtener más información, consulte el [sección Livy](https://spark.rstudio.com/guides/distributed-r/#livy) de la documentación de sparklyr en cálculos R distribuidos. Con esta configuración, solo puede usar los paquetes de R que ya están instalados en el clúster de Spark en el código de R que se pasa a **spark_apply**. El ejemplo siguiente muestra esta funcionalidad:

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de datos de gran tamaño, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos](big-data-cluster-overview.md).