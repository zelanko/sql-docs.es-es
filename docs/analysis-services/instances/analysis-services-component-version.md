---
title: Comprobar la versión de compilación de actualización acumulativa de SQL Server Analysis Services | Microsoft Docs
ms.date: 07/11/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1da8384bb51360178e1735d13f6c6b706e8b7ff
ms.sourcegitcommit: 87efa581f7d4d84e9e5c05690ee1cb43bd4532dc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38999362"
---
# <a name="verify-analysis-services-cumulative-update-build-version"></a>Comprobar la versión de compilación de actualización acumulativa de Analysis Services

A partir de SQL Server 2017, el número de versión de compilación de Analysis Services y el número de versión de compilación de motor de base de datos de SQL Server no coinciden. Aunque Analysis Services y el motor de base de datos utilizan el mismo programa de instalación, los sistemas de compilación cada uso son independientes.

 En algunos casos, puede ser necesario comprobar si se ha aplicado un paquete de compilación de la actualización acumulativa (CU) y se han actualizado los componentes de Analysis Services. Puede comprobar al comparar los números de versión de compilación de archivos de componentes de Analysis Services instalados en el equipo con los números de versión de compilación para una determinada unidad de capacidad.

## <a name="verify-component-file-version"></a>Comprobar la versión del archivo de componente

Para comprobar la versión del archivo de componente 

1. Vaya a [versiones de compilación de SQL Server 2017](https://support.microsoft.com/help/4047329). 
2. En **compilaciones de SQL Server 2017 actualización acumulativa (CU)**, haga clic en el **número de Knowledge Base** para la compilación que desea comprobar.
3. En el **actualización acumulativa (#) para SQL Server 2017** artículo, en el **información del paquete de actualización acumulativa** sección, expanda **información de archivo del paquete de actualización acumulativa**.
4. En el **SQL Server 2017 Analysis Services** de tabla, compruebe la versión del archivo para el **msmdsrv.exe** archivo del componente. Si se ha aplicado la CU, el número de versión del archivo debe coincidir con el archivo msmdsrv.exe instalado en el equipo.

## <a name="see-also"></a>Vea también  

[Instalar actualizaciones de servicio de SQL Server](../../database-engine/install-windows/install-sql-server-servicing-updates.md)  

[Centro de actualización para Microsoft SQL Server](https://msdn.microsoft.com/library/ff803383.aspx)
  
  
