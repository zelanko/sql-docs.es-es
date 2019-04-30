---
title: Objeto DataControl (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl
- RDS.DataControl
helpviewer_keywords:
- DataControl object [ADO]
ms.assetid: d85ea4fc-451c-436e-97b8-58f92b149dd0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aa05b8b4be3c155c7ca59132892e0863dda60a5f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63134419"
---
# <a name="datacontrol-object-rds"></a>Objeto DataControl (RDS)
Enlaza una consulta de datos [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) a uno o varios controles (por ejemplo, un cuadro de texto, control de cuadrícula o cuadro combinado) para mostrar el **Recordset** datos en una página Web.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>Comentarios  
 El identificador de clase para el **RDS. DataControl** objeto es BD96C556-65A3 - 11 D 0-983A-00C04FC29E33.  
  
> [!NOTE]
>  Si se produce un error que un [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) o **RDS. DataControl** object no carga, asegúrese de que está usando el identificador de clase correcto. La clase identificadores para estos objetos han cambiado desde la versión 1.0 y 1.1. Además, tenga cuidado de que se deben establecer las columnas aceptan valores NULL incluso cuando se usa el **RDS DataControl** objeto.  
  
 Para un escenario básico, deberá establecer solo la **SQL**, **Connect**, y **Server** propiedades de la **RDS. DataControl** objeto, que llamará automáticamente el objeto de negocios de forma predeterminada, [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md).  
  
 Todas las propiedades de la **RDS. DataControl** son opcionales porque los objetos de negocios personalizada pueden reemplazar su funcionalidad.  
  
> [!NOTE]
>  Si una consulta para varios resultados, solo las primeras [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) se devuelve. Si se necesitan varios conjuntos de resultados, asigne cada uno a su propio **DataControl**. Un ejemplo de una consulta para varios resultados podría ser la siguiente: `"Select * from Authors, Select * from Topics"`  
  
 Adición de "DFMode = 20;" a la cadena de conexión cuando usas el **RDS. DataControl** objeto puede mejorar el rendimiento del servidor al actualizar los datos. Con esta configuración, el **RDSServer.DataFactory** objeto en el servidor usa un modo menos intensivo de recursos. Sin embargo, las siguientes características no están disponibles en esta configuración:  
  
-   Usar consultas parametrizadas.  
  
-   Obtención de información de parámetro o columna antes de llamar a la **Execute** método.  
  
-   Establecer **Transact actualizaciones** a **True**.  
  
-   Al obtener el estado de fila.  
  
-   Una llamada a la [Resync](../../../ado/reference/ado-api/resync-method.md) método.  
  
-   Actualización (de forma explícita o automáticamente) a través de la [Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) propiedad.  
  
-   Establecer **comando** o [Recordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) propiedades.  
  
-   Uso de **adCmdTableDirect**.  
  
 El **RDS. DataControl** objeto se ejecuta en modo asincrónico de forma predeterminada. Si necesita una ejecución sincrónica de la aplicación, establezca el [ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md) igual al parámetro **adcExecSync** y [FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md) parámetro igual a **adcFetchUpFront**, como se muestra en el ejemplo siguiente.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 Utilice uno **RDS. DataControl** objeto para vincular los resultados de una sola consulta a uno o más controles visuales. Por ejemplo, suponga que codifica una consulta que solicita datos de cliente, como el nombre, residencia, lugar de nacimiento, edad y estado de prioridad. Puede usar una sola **RDS. DataControl** objeto para mostrar el nombre, la edad y la región de un cliente en tres cuadros de texto independiente. Estado de prioridad en una casilla de verificación; y todos los datos de un control de cuadrícula.  
  
 Usar diferentes **RDS. DataControl** objetos para vincular los resultados de varias consultas a controles visuales diferentes. Por ejemplo, suponga que utiliza una consulta para obtener información acerca de un cliente y una segunda consulta para obtener información sobre los productos que el cliente ha adquirido. Desea mostrar los resultados de la primera consulta en tres cuadros de texto y una casilla de verificación y los resultados de la segunda consulta en un control de cuadrícula. Si usa el objeto de negocios de forma predeterminada (**RDSServer.DataFactory**), debe hacer lo siguiente:  
  
-   Agregue dos **RDS. DataControl** objetos a la página Web.  
  
-   Escribir dos consultas, una para cada **SQL** propiedad de los dos **RDS. DataControl** objetos. Una **RDS. DataControl** objeto contendrá una consulta SQL que se solicita información del cliente; el segundo contendrá una consulta que solicita una lista de mercancía, el cliente ha adquirido.  
  
-   En las etiquetas de objeto de cada control enlazado, especifique el valor DATAFLD para establecer los valores para los datos que desea mostrar en cada control visual.  
  
 No hay ninguna restricción de recuento del número de **RDS. DataControl** objetos que puede insertar mediante etiquetas de objeto en una única página Web.  
  
 Al definir el **RDS. DataControl** objetos en una página Web, utilice distinto de cero **alto** y **ancho** valores como 1 (para evitar la inclusión de espacio adicional).  
  
 Componentes de cliente de servicio de datos remota ya se incluyen como parte de Internet Explorer 4.0; por lo tanto, no es necesario incluir un parámetro de código base en su **RDS. DataControl** etiqueta de objeto.  
  
 Con Internet Explorer 4.0 o posterior, puede enlazar a datos mediante el uso de controles HTML y los controles ActiveX® sólo si están marcados como controles de modelo apartamento.  
  
> [!NOTE]
>  **Los usuarios de Microsoft Visual Basic** el **RDS. DataControl** es seguro para scripting y solo se usa en las aplicaciones basadas en Web. Una aplicación de cliente de Visual Basic no tiene es necesario para él.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del objeto DataControl (VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)






















