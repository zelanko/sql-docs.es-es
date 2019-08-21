---
title: Usar sparklyr de RStudio
titleSuffix: SQL Server big data clusters
description: Conéctese al clúster de Big Data mediante sparklyr desde RStudio.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d23ce447f097d092059f7298ca5478ed6c3f19fc
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653322"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>Uso de sparklyr en SQL Server clúster de Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr proporciona una interfaz R para Apache Spark. Sparklyr es una forma popular para que los desarrolladores de R usen Spark. En este artículo se describe cómo usar sparklyr en [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] un con RStudio.

## <a name="prerequisites"></a>Requisitos previos

- [Implemente un clúster de macrodatos SQL Server 2019](quickstart-big-data-cluster-deploy.md).

### <a name="install-rstudio-desktop"></a>Instalación de RStudio Desktop

Instale y configure **RStudio Desktop** con los pasos siguientes:

1. Si está ejecutando en un cliente Windows, [Descargue e instale R 3.4.4](https://cran.rstudio.com/bin/windows/base/old/3.4.4).

1. [Descargue e instale RStudio Desktop](https://www.rstudio.com/products/rstudio/download/).

1. Una vez finalizada la instalación, ejecute los siguientes comandos dentro de RStudio Desktop para instalar los paquetes necesarios:

   ```RStudioDesktop
   install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## <a name="connect-to-spark-in-a-big-data-cluster"></a>Conexión a Spark en un clúster de Big Data

Puede usar sparklyr para conectarse desde un cliente al clúster de Big Data mediante Livy y la puerta de enlace de HDFS/Spark. 

En RStudio, cree un script de R y conéctese a Spark como en el ejemplo siguiente:

> [!TIP]
> Para los `<USERNAME>` valores `<PASSWORD>` y, use el nombre de usuario (por ejemplo, raíz) y la contraseña que estableció durante la implementación del clúster de Big Data. Para los `<IP>` valores `<PORT>` y, vea la documentación sobre [cómo conectarse a un clúster de Big Data](connect-to-big-data-cluster.md).

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

Después de conectarse a Spark, puede ejecutar sparklyr. En el ejemplo siguiente se realiza una consulta en el conjunto de elementos de iris mediante sparklyr:

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>Cálculos de R distribuidos

Una característica de sparklyr es la capacidad de [distribuir los cálculos de R](https://spark.rstudio.com/guides/distributed-r/) con [spark_apply](https://spark.rstudio.com/reference/spark_apply/).

Dado que los clústeres de Big Data usan conexiones Livy, `packages = FALSE` debe establecer en la llamada a **spark_apply**. Para obtener más información, consulte la [sección Livy](https://spark.rstudio.com/guides/distributed-r/#livy) de la documentación de sparklyr sobre los cálculos de R distribuidos. Con esta configuración, solo puede usar los paquetes de R que ya están instalados en el clúster de Spark en el código de R que se pasa a **spark_apply**. En el ejemplo siguiente se muestra esta funcionalidad:

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos, vea [Qué son [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] ](big-data-cluster-overview.md).
