---
title: Códigos de Error de objeto DataControl | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], DataControl
- DataControl errors [ADO]
ms.assetid: 293df9d5-e1a2-406d-9107-07bf7cdc6f96
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7cf56b6614587c333f473136f1cafc72128846a2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52514384"
---
# <a name="datacontrol-object-error-codes"></a>Códigos de Error de objeto DataControl
La siguiente tabla se enumeran los [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) códigos de error de objeto. La conversión de decimal positiva de los dos bytes bajos, la traducción decimal negativo del código de error completo y los valores hexadecimales se muestran.

|RDS. Códigos de error de control de datos|Number|Descripción|
|---------------------------------|------------|-----------------|
|**IDS_AsyncPending**|4107-2146824175 0x800A1011|No se puede realizar la operación mientras la operación asincrónica está pendiente.|
|**IDS_BadInlineTablegram**|de 4105-2146824183 0x800A1009|Tablegram mal alineado.|
|**IDS_CantConnect**|4099-2146824189 0x800A1003|No se puede conectar al servidor.|
|**IDS_CantCreateObject**|4100-2146824188 0x800A1004|No se puede crear el objeto de negocios.|
|**IDS_CantFindDataspace**|4102-2146824186 0x800A1006|La propiedad DataSpace no es válida.|
|**IDS_CantInvokeMethod**|4101-2146824187 0x800A1005|No se puede invocar el método en el objeto de negocios.|
|**IDS_CrossDomainWarning**|4112-2146824170 0x800A1016|Esta página tiene acceso a datos en otro dominio. ¿Desea permitir esto? Para evitar este mensaje en Internet Explorer, puede agregar un sitio Web seguro a la zona de sitios de confianza en el **seguridad** pestaña de la **opciones de Internet** cuadro de diálogo.|
|**IDS_InvalidADCClientVersion**|4106-2146824176 0x800A1010|Versión no válida de cliente RDS - cliente es más reciente que el servidor.|
|**IDS_INVALIDARG**|5376-2147019520 0x80071500|Uno o más argumentos no son válidos.|
|**IDS_InvalidBindings**|4097-2146824191 0x800A1001|Error en la propiedad de enlaces.|
|**IDS_InvalidParam**|4110-2146824172 0x800A1014|Uno o más argumentos no son válidos.|
|**IDS_NOINTERFACE**|5377-2147019519 0x80071501|Interfaz no se admite.|
|**IDS_NotReentrant**|4111-2146824171 0x800A1015|Solicitud no se puede ejecutar mientras todavía está procesando el controlador de eventos.|
|**IDS_ObjectNotSafe**|4103-2146824185 0x800A1007|Configuración de seguridad en este equipo prohíbe la creación del objeto de negocios.|
|**IDS_RecordsetNotOpen**|4109-2146824173 0x800A1013|**Conjunto de registros** no está abierto.|
|**IDS_ResetInvalidField**|4108-2146824174 0x800A1012|La columna especificada en **SortColumn** o **FilterColumn** no existe.|
|**IDS_RowsetNotUpdateable**|4104-2146824184 0x800A1008|Conjunto de filas no se puede actualizar.|
|**IDS_UnexpectedError**|4351-2146823937 0x800A10FF|Error inesperado.|
|**IDS_UpdatesFailed**|4098-2146824190 0x800A1002|No se puede actualizar la base de datos.|
|**IDS_URLMONNotFound**|4119-2146824169 0x800A1017|DataControl **URL** propiedad requiere Urlmon.dll, que no se encuentra el archivo del sistema.|

## <a name="see-also"></a>Vea también
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)
