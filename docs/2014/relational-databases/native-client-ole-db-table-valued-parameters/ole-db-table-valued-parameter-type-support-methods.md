---
title: Compatibilidad con tipos de parámetro con valores de tabla de OLE DB (métodos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (methods)
ms.assetid: e3c2a450-8fd4-44cb-93d8-affe1b65c68e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3f0ea289b75085cd4b7e90531eeaf592979707c2
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704645"
---
# <a name="ole-db-table-valued-parameter-type-support-methods"></a>Compatibilidad con tipos de parámetro con valores de tabla de OLE DB (métodos)
  Los siguientes métodos OLE DB estándar admiten parámetros con valores de tabla:  
  
|Método|Compatibilidad con parámetros con valores de tabla|  
|------------|-------------------------------------|  
|ITableDefinitionWithConstraints::CreateTableWithConstraints|Se utiliza cuando se conoce la información de tipo del parámetro con valores de tabla y se desea crear instancias de un objeto de conjunto de filas de parámetro con valores de tabla basado en la información de tipo.<br /><br /> Para más información, consulte "Escenario estático" en [Creación de conjuntos de filas de parámetros con valores de tabla](table-valued-parameter-rowset-creation.md).|  
|IOpenRowset::OpenRowset|Se utiliza cuando no se conoce la información de tipo de un parámetro con valores de tabla y se desea crear instancias de un objeto de conjunto de filas de parámetro con valores de tabla basado en información de metadatos recuperada del servidor.<br /><br /> Para más información, consulte "Escenario dinámico" en [Creación de conjuntos de filas de parámetros con valores de tabla](table-valued-parameter-rowset-creation.md).|  
|ISSCommandWithParameters::SetParameterInfo|Para especificar un parámetro de comandos de parámetro con valores de tabla, el consumidor especifica el tipo del parámetro como "table" o "DBTYPE_TABLE" en el miembro *pwszName* de la estructura DBPARAMBINDINFO. *ulParamSize* se establece en ~0. Para más información, consulte "Especificación de parámetros con valores de tabla" en [Ejecutar comandos que contienen parámetros con valores de tabla](executing-commands-containing-table-valued-parameters.md).|  
|ISSCommandWithParameters::SetParameterProperties|Establece propiedades específicas de parámetros con valores de tabla, tales como el nombre de esquema, nombre de tipo, orden de columnas y columnas predeterminadas.<br /><br /> El consumidor especifica el ordinal del parámetro en *iOrdinal* de la estructura SSPARAMPROPS. El conjunto de propiedades solicitado es DBPROPSET_SQLSERVERPARAMETER.|  
|ISSCommandWithParameters::GetParameterInfo|Obtiene los tipos de todos los parámetros para un comando especificado.<br /><br /> Para los parámetros con valores de tabla, el campo *wType* de la estructura DBPARAMINFO tendrá el tipo DBTYPE_TABLE. El campo *ulParamSize* se establecerá en ~0 para indicar longitud desconocida.|  
|ISSCommandWithParameters::GetParameterProperties|Obtiene información de tipo adicional para parámetros del tipo DBTYPE_TABLE.<br /><br /> El consumidor especifica el ordinal del parámetro en el miembro *iOrdinal* de la estructura SSPARAMPROPS. El consumidor puede solicitar cualquiera de las propiedades del conjunto de propiedades DBPROPSET_SQLSERVERPARAMETER que se enumeran en ISSCommandWithParameters::SetParameterProperties.<br /><br /> Dado que el consumidor no conoce el tipo de parámetro con valores de tabla, el proveedor debe establecer SSPROP_PARAM_TYPE_TYPENAME, SSPROP_PARAM_TYPE_SCHEMANAME y SSPROP_PARAM_TYPE_CATALOGNAME en sus valores correctos. Las propiedades restantes, SSPROP_PARAM_TABLE_DEFAULT_COLUMNS y SSPROP_PARAM_TABLE_COLUMN_SORT_ORDER, tendrán sus valores predeterminados. Cuando el consumidor ha detectado el nombre de tipo del parámetro con valores de tabla, usa IOpenRowset::OpenRowset para crear una instancia de este parámetro con valores de tabla, especificando el nombre de tipo de parámetro con valores de tabla. Para más información, consulte [Detección de tipos de parámetros con valores de tabla](../../database-engine/dev-guide/table-valued-parameter-type-discovery.md).|  
|IRowsetInfo::GetProperties|Obtiene propiedades de conjunto de filas de parámetro con valores de tabla. El consumidor puede utilizar estas propiedades para configurar óptimamente los enlaces.|  
|IColumnsRowset::GetColumnsRowset|Recupera información de metadatos sobre una tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para los parámetros con valores de tabla, esta misma interfaz proporciona información de metadatos detallada sobre cada columna, como a continuación:<br /><br /> -DBCOLUMN_FLAGS indica la nulabilidad a través del bit de DBCOLUMNFLAGS_ISNULLABLE.<br />-DBCOLUMN_ISUNIQUE indica si la columna es una columna de identidad.<br />-DBCOLUMN_COMPUTEMODE indica si la columna es calculada.|  
|IAccessor::CreateAccessor|Para enlazar un objeto de conjunto de filas de parámetro con valores de tabla a un parámetro de comandos, cree un descriptor de acceso con su miembro *wType* establecido en DBTYPE_TABLE. La estructura DBOBJECT contendrá IID_IRowset o cualquier otra interfaz de objeto de conjunto de filas válida en el miembro *iid*. El resto de los campos se trata de igual forma que DBTYPE_IUNKNOWN.|  
  
## <a name="see-also"></a>Consulte también  
 [OLE DB compatibilidad con tipos de parámetros con valores de tabla](ole-db-table-valued-parameter-type-support.md)   
 [Creación de conjuntos de filas de parámetros con valores de tabla](table-valued-parameter-rowset-creation.md)   
 [Usar parámetros con valores de tabla &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)  
  
  
