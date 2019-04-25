---
title: 'biblioteca de funciones de R olapR: SQL Server Machine Learning Services'
description: Introducción a la biblioteca de funciones olapR en SQL Server 2016 R Services y SQL Server 2017 Machine Learning Services con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e5419900b8ba573ec0658a5022be68105b0b8607
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641850"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR (biblioteca de R en SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**olapR** es una biblioteca de Microsoft de las funciones de R que se utiliza para consultas MDX en un cubo OLAP de SQL Server Analysis Services. Las funciones no admiten todas las operaciones de MDX, pero puede generar consultas de ese segmento, desglosar, obtención de detalles, paquete acumulativo de actualizaciones y en las dimensiones de tabla dinámica. 

Este paquete no se haya cargado previamente en una sesión de R. Ejecute el siguiente comando para cargar la biblioteca.

```R
library(olapR)
```

Puede usar esta biblioteca en las conexiones a un cubo OLAP de Analysis Services en todas las versiones compatibles de SQL Server. No se admiten las conexiones a un modelo tabular en este momento.

## <a name="package-version"></a>Versión del paquete

Versión actual es 1.0.0 en todos los productos de Windows sólo y descargas que proporciona la biblioteca.

## <a name="full-reference-documentation"></a>Documentación de referencia completa

El **olapr** library se distribuye en varios productos de Microsoft, pero el uso es el mismo si obtener la biblioteca de SQL Server u otro producto. Dado que las funciones son los mismos, [documentación para las funciones individuales sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) se publica en una sola ubicación en la [referencia R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Debe cualquier producto específico comportamientos existen, se anotará discrepancias en la página de Ayuda de la función.

## <a name="availability-and-location"></a>Disponibilidad y la ubicación

Este paquete se proporciona en los siguientes productos, así como en varias imágenes de máquinas virtuales en Azure. Ubicación del paquete varía según corresponda.

Producto | Location |
--------|----------|
SQL Server 2017 Machine Learning Services (con la integración de R) | C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Program Files\Microsoft\R_SERVER\library |
Cliente de Microsoft R | C:\Program Files\Microsoft\R Client\R_SERVER\library |
Data Science Virtual Machine (en Azure) | C:\Program Files\Microsoft\R Client\R_SERVER\library |
Máquina Virtual SQL Server (en Azure) <sup>1</sup> | C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> integración de R es opcional en SQL Server. La biblioteca olapR se instalará cuando se agrega la característica de R o Machine Learning durante la configuración de máquina virtual.


## <a name="see-also"></a>Vea también

[Cómo crear consultas MDX con olapR](how-to-create-mdx-queries-using-olapr.md)
