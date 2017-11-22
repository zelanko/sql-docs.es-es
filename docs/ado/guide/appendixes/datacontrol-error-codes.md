---
title: "Códigos de Error de DataControl | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- errors [ADO], DataControl
- DataControl errors [ADO]
ms.assetid: 293df9d5-e1a2-406d-9107-07bf7cdc6f96
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 54dcd3721781ccb2889d88c2545d8bb3630cb7bc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="datacontrol-object-error-codes"></a>Códigos de Error de objeto DataControl
La siguiente tabla se recogen los [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) códigos de error del objeto. La conversión decimal positiva de los dos bytes bajos, la traducción decimal negativa del código de error completo y los valores hexadecimales se muestran.

|RDS. Códigos de error de DataControl|Number|Description|
|---------------------------------|------------|-----------------|
|**IDS_AsyncPending**|4107-2146824175 0x800A1011|No se puede realizar la operación mientras está pendiente una operación asincrónica.|
|**IDS_BadInlineTablegram**|4105-2146824183 0x800A1009|Tablegram en línea incorrecta.|
|**IDS_CantConnect**|4099-2146824189 0x800A1003|No se puede conectar al servidor.|
|**IDS_CantCreateObject**|4100-2146824188 0x800A1004|No se puede crear el objeto de negocios.|
|**IDS_CantFindDataspace**|4102-2146824186 0x800A1006|Propiedad DataSpace no es válida.|
|**IDS_CantInvokeMethod**|4101-2146824187 0x800A1005|No se puede invocar el método en el objeto de negocios.|
|**IDS_CrossDomainWarning**|4112-2146824170 0x800A1016|Esta página tiene acceso a datos en otro dominio. ¿Desea permitir esto? Para evitar este mensaje en Internet Explorer, puede agregar un sitio Web seguro a la zona de sitios de confianza en el **seguridad** pestaña de la **opciones de Internet** cuadro de diálogo.|
|**IDS_InvalidADCClientVersion**|4106-2146824176 0x800A1010|Versión de cliente RDS no válida: El cliente es más reciente que el servidor.|
|**IDS_INVALIDARG**|5376-2147019520 0x80071500|Uno o más argumentos no son válidos.|
|**IDS_InvalidBindings**|4097-2146824191 0x800A1001|Error en la propiedad de enlaces.|
|**IDS_InvalidParam**|4110-2146824172 0x800A1014|Uno o más argumentos no son válidos.|
|**IDS_NOINTERFACE**|5377-2147019519 0x80071501|Interfaz no es compatible.|
|**IDS_NotReentrant**|4111-2146824171 0x800A1015|No se puede ejecutar la solicitud mientras todavía está procesando el controlador de eventos.|
|**IDS_ObjectNotSafe**|4103-2146824185 0x800A1007|Configuración de seguridad en este equipo prohíbe la creación de objeto de negocios.|
|**IDS_RecordsetNotOpen**|4109-2146824173 0x800A1013|**Conjunto de registros** no está abierto.|
|**IDS_ResetInvalidField**|4108-2146824174 0x800A1012|Las columnas especificadas en **SortColumn** o **FilterColumn** no existe.|
|**IDS_RowsetNotUpdateable**|4104-2146824184 0x800A1008|El conjunto de filas no se puede actualizar.|
|**IDS_UnexpectedError**|4351-2146823937 0x800A10FF|Error inesperado.|
|**IDS_UpdatesFailed**|4098-2146824190 0x800A1002|No se puede actualizar la base de datos.|
|**IDS_URLMONNotFound**|4119-2146824169 0x800A1017|DataControl **URL** propiedad requiere el archivo del sistema Urlmon.dll, pero no se encuentra.|

## <a name="see-also"></a>Vea también
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)
