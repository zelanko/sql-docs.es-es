---
title: No incluye características de Master Data Services en SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3236cce0-cfd9-43f8-8be3-e8c8dff8f162
caps.latest.revision: 12
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: f2e9a15b4a0f1441d63ab39a4b65861fcfef099e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167056"
---
# <a name="discontinued-master-data-services-features-in-sql-server-2014"></a>Características descontinuadas de Master Data Services en SQL Server 2014
  Este tema describe las características de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que ya no están disponibles en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="includesssql14includessssql14-mdmd-discontinued-features"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Características no incluidas  
 Hay características que no se incluyen en esta versión.  
  
## <a name="includesssql11includessssql11-mdmd-discontinued-features"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Características no incluidas  
  
### <a name="security"></a>Seguridad  
 Para facilitar la seguridad de asignación, ya no se pueden asignar permisos de objeto del modelo a la jerarquía derivada, la jerarquía explícita y los objetos del grupo de atributos.  
  
-   Los permisos de jerarquía derivada se basan ahora en el modelo. Por ejemplo, si desea que un usuario tenga permiso para una jerarquía derivada, debe asignar **actualización** al objeto de modelo. A continuación, puede asignar **Deny** acceso a todas las entidades que no desea que el usuario debe tener acceso.  
  
-   Los permisos de jerarquía explícita se basan ahora en la entidad. Por ejemplo, si el usuario tiene **actualización** permisos para una entidad de cuenta, a continuación, todas las jerarquías explícitas para la entidad se pueden actualizables.  
  
-   Ya no se pueden asignar permisos de grupo de atributos en el **permisos de usuario y grupo** área funcional. En su lugar, en el **administración del sistema** área funcional que se crean grupos de atributos, los usuarios y grupos pueden proporcionarse **actualización** permisos a grupos de atributos. **Solo lectura** permisos a grupos de atributos ya no está disponible.  
  
### <a name="staging-process"></a>Proceso de almacenamiento provisional  
 No puede usar el nuevo proceso de almacenamiento provisional para:  
  
-   Crear o eliminar colecciones.  
  
-   Agregar o quitar miembros de colecciones.  
  
-   Reactivar miembros y colecciones.  
  
 Puede usar el proceso de almacenamiento provisional de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] para trabajar con colecciones.  
  
### <a name="model-deployment-wizard"></a>Asistente para la implementación de modelos  
 Los paquetes que contienen datos ya no se pueden crear e implementar mediante el asistente en la aplicación web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. En su lugar se puede usar una nueva utilidad de la línea de comandos. Para obtener más información, consulte [Implementar modelos &#40;Master Data Services&#41;](deploying-models-master-data-services.md).  
  
 El asistente se puede seguir usando para crear e implementar paquetes que no contienen datos.  
  
 Además, los paquetes solamente se pueden implementar en la edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en la que se crearon. Esto significa que los paquetes que se hayan creado en [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] no se pueden implementar en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Debe implementar el paquete en un entorno de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] y, posteriormente, actualizar la base de datos a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
### <a name="code-generation-business-rules"></a>Reglas de negocios de generación de código  
 Las reglas de negocios que generan valores automáticamente para el atributo Código se administran ahora de manera diferente. Anteriormente, para generar valores para el atributo de código, usar el **atributo predeterminado para un valor generado** acción en el **administración del sistema** área funcional en **las reglas de negocios** . Ahora, en **administración del sistema**, debe editar la entidad para habilitar valores código generados automáticamente. Para obtener más información, consulte [Creación automática de código &#40;Master Data Services&#41;](automatic-code-creation-master-data-services.md).  
  
 Si tiene un paquete de implementación de modelo de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] que contenga una regla de este tipo, al actualizar la base de datos a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] se excluirá la regla de negocios.  
  
### <a name="bulk-updates-and-exporting"></a>Actualizaciones y exportación masivas  
 En la aplicación web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], ya no se pueden actualizar los valores de atributo para varios miembros de forma masiva. Para realizar actualizaciones masivas, utilice el proceso de almacenamiento provisional o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].  
  
 En la aplicación web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], ya no se pueden exportar miembros a Excel. Para trabajar con miembros en Excel, use el [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].  
  
### <a name="transactions"></a>Transactions  
 En el **Explorer** área funcional, ya no los usuarios pueden revertir sus propias transacciones. Anteriormente, los usuarios podían revertir los cambios realizados a los datos en **Explorer**. Los administradores pueden seguir invirtiendo transacciones para todos los usuarios en el **administración de versiones** área funcional.  
  
 Ahora las anotaciones son permanentes y no se pueden eliminar. Anteriormente, las anotaciones se consideraban transacciones y podían eliminarse invirtiendo la transacción.  
  
### <a name="web-service"></a>Servicio web  
 Ahora el servicio web de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] se habilita automáticamente, tal como requiere Silverlight. Anteriormente, el servicio web tenía que habilitarse manualmente.  
  
### <a name="powershell-cmdlets"></a>Cmdlets de PowerShell  
 MDS ya no incluye los cmdlets de PowerShell.  
  
## <a name="see-also"></a>Vea también  
 [Características desusadas de Master Data Services en SQL Server 2014](deprecated-master-data-services-features.md)  
  
  
