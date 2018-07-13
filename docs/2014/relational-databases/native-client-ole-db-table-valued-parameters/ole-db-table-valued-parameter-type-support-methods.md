---
title: Compatibilidad con el tipo parámetros con valores de tabla OLE DB (métodos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (methods)
ms.assetid: e3c2a450-8fd4-44cb-93d8-affe1b65c68e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eebe58ccc32e7440505237730b062ff9b6056ef0
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411224"
---
# <a name="ole-db-table-valued-parameter-type-support-methods"></a>Compatibilidad con tipos de parámetro con valores de tabla de OLE DB (métodos)
  Los siguientes métodos OLE DB estándar admiten parámetros con valores de tabla:  
  
|Método|Compatibilidad con parámetros con valores de tabla|  
|------------|-------------------------------------|  
|ITableDefinitionWithConstraints::CreateTableWithConstraints|Se utiliza cuando se conoce la información de tipo del parámetro con valores de tabla y se desea crear instancias de un objeto de conjunto de filas de parámetro con valores de tabla basado en la información de tipo.<br /><br /> Para obtener más información, vea "Escenario estático" en [creación de conjuntos de filas de parámetros con valores de tabla](table-valued-parameter-rowset-creation.md).|  
|IOpenRowset::OpenRowset|Se utiliza cuando no se conoce la información de tipo de un parámetro con valores de tabla y se desea crear instancias de un objeto de conjunto de filas de parámetro con valores de tabla basado en información de metadatos recuperada del servidor.<br /><br /> Para obtener más información, vea "Escenario dinámico" en [creación de conjuntos de filas de parámetros con valores de tabla](table-valued-parameter-rowset-creation.md).|  
|ISSCommandWithParameters::SetParameterInfo|Para especificar un parámetro de comando de parámetro con valores de tabla, el consumidor especifica el tipo del parámetro como "table" o "DBTYPE_TABLE" en el *pwszName* miembro de estructura DBPARAMBINDINFO. El *ulParamSize* se establece en ~ 0. Para obtener más información, vea "Especificación del parámetro con valores de tabla" en [Executing Commands Containing Table-Valued parámetros](executing-commands-containing-table-valued-parameters.md).|  
|Isscommandwithparameters:: SetParameterProperties|Establece propiedades específicas de parámetros con valores de tabla, tales como el nombre de esquema, nombre de tipo, orden de columnas y columnas predeterminadas.<br /><br /> El consumidor especifica el ordinal del parámetro en el *iOrdinal* de la estructura SSPARAMPROPS. El conjunto de propiedades solicitado es DBPROPSET_SQLSERVERPARAMETER.|  
|ISSCommandWithParameters::GetParameterInfo|Obtiene los tipos de todos los parámetros para un comando especificado.<br /><br /> Para los parámetros con valores de tabla, el *wType* campo en la estructura DBPARAMINFO tendrá tipo DBTYPE_TABLE. El *ulParamSize* campo se establecerá en ~ 0 para indicar longitud desconocida.|  
|Isscommandwithparameters:: Getparameterproperties|Obtiene información de tipo adicional para parámetros del tipo DBTYPE_TABLE.<br /><br /> El consumidor especifica el ordinal del parámetro en el *iOrdinal* miembro de la estructura SSPARAMPROPS. El consumidor puede solicitar cualquiera de las propiedades de la propiedad DBPROPSET_SQLSERVERPARAMETER establecida que aparecen en isscommandwithparameters:: SetParameterProperties.<br /><br /> Dado que el consumidor no conoce el tipo de parámetro con valores de tabla, el proveedor debe establecer SSPROP_PARAM_TYPE_TYPENAME, SSPROP_PARAM_TYPE_SCHEMANAME y SSPROP_PARAM_TYPE_CATALOGNAME en sus valores correctos. Las propiedades restantes, SSPROP_PARAM_TABLE_DEFAULT_COLUMNS y SSPROP_PARAM_TABLE_COLUMN_SORT_ORDER, tendrán sus valores predeterminados. Después de que el consumidor ha detectado el nombre del tipo de parámetro con valores de tabla, utiliza IOpenRowset:: OpenRowset para crear una instancia de este parámetro con valores de tabla, especificando el nombre del tipo de parámetro con valores de tabla. Para obtener más información, consulte [detección de tipos de parámetro con valores de tabla](../../database-engine/dev-guide/table-valued-parameter-type-discovery.md).|  
|IRowsetInfo:: GetProperties|Obtiene propiedades de conjunto de filas de parámetro con valores de tabla. El consumidor puede utilizar estas propiedades para configurar óptimamente los enlaces.|  
|IColumnsRowset::GetColumnsRowset|Recupera información de metadatos sobre una tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para los parámetros con valores de tabla, esta misma interfaz proporciona información de metadatos detallada sobre cada columna, como a continuación:<br /><br /> -DBCOLUMN_FLAGS indica nulabilidad a través del bit DBCOLUMNFLAGS_ISNULLABLE.<br />-DBCOLUMN_ISUNIQUE indica si la columna es una columna de identidad.<br />-DBCOLUMN_COMPUTEMODE indica si la columna es calculada.|  
|IAccessor:: CreateAccessor|Para enlazar un objeto de conjunto de filas de parámetro con valores de tabla a un parámetro de comando, crea un descriptor de acceso con su *wType* miembro establecido en DBTYPE_TABLE. La estructura DBOBJECT contendrá IID_IRowset o cualquier otra interfaz de objeto de conjunto de filas válida en el *iid* miembro. El resto de los campos se trata de igual forma que DBTYPE_IUNKNOWN.|  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con tipos de parámetro con valores de tabla OLE DB](ole-db-table-valued-parameter-type-support.md)   
 [Creación del conjunto de filas de parámetro con valores de tabla](table-valued-parameter-rowset-creation.md)   
 [Usar parámetros con valores de tabla &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)  
  
  
