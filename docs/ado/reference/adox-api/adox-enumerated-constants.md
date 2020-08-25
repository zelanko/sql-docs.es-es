---
description: Constantes enumeradas de ADOX
title: Constantes enumeradas de ADOX | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerated constants [ADOX]
ms.assetid: 9d91f511-d46f-44ef-97ef-77bf93836186
author: rothja
ms.author: jroth
ms.openlocfilehash: 553924a51845c7ac49bfb76bab27f75c7d4e4742
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771614"
---
# <a name="adox-enumerated-constants"></a>Constantes enumeradas de ADOX
Para ayudar a la depuración, las constantes enumeradas de ADOX muestran un valor para cada constante. Sin embargo, este valor es meramente consultivo y puede cambiar de una versión de ADOX a otra. El código solo debe depender del nombre, no del valor real, de las constantes enumeradas.  
  
 Se definen las constantes enumeradas siguientes.  
  
|Enumeración|Descripción|  
|-----------------|-----------------|  
|[ActionEnum](./actionenum.md)|Especifica el tipo de acción que se debe realizar cuando se llama a **SetPermissions** .|  
|[AllowNullsEnum](./allownullsenum.md)|Especifica si los registros con valores NULL se indizan.|  
|[ColumnAttributesEnum](./columnattributesenum.md)|Especifica las características de una **columna**.|  
|[DataTypeEnum](../ado-api/datatypeenum.md)|Especifica el tipo de datos de un **campo**, un **parámetro**o una **propiedad**.|  
|[InheritTypeEnum](./inherittypeenum.md)|Especifica cómo los objetos heredarán los permisos establecidos con **SetPermissions**.|  
|[KeyTypeEnum](./keytypeenum.md)|Especifica el tipo de **clave**: principal, externa o única.|  
|[ObjectTypeEnum](./objecttypeenum.md)|Especifica el tipo de objeto de base de datos para el que se van a establecer permisos o propiedad.|  
|[RightsEnum](./rightsenum.md)|Especifica los derechos o permisos para un grupo o usuario en un objeto.|  
|[RuleEnum](./ruleenum.md)|Especifica la regla que se debe seguir cuando se elimina una **clave** .|  
|[SortOrderEnum](./sortorderenum.md)|Especifica la secuencia de ordenación para una columna indizada.|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API de ADOX](./adox-object-model.md?view=sql-server-ver15)   
 [Extensiones de ADO para lenguaje de definición de datos y seguridad (ADOX)](../../guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)