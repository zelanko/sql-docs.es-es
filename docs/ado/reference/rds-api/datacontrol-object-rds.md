---
title: Objeto DataControl (RDS) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl
- RDS.DataControl
helpviewer_keywords:
- DataControl object [ADO]
ms.assetid: d85ea4fc-451c-436e-97b8-58f92b149dd0
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c1ca22f1a9573ba9f3e01a557eb64f2cb5f4f841
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="datacontrol-object-rds"></a>Objeto DataControl (RDS)
Enlaza una consulta de datos [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) a uno o varios controles (por ejemplo, un cuadro de texto, el control de cuadrícula o cuadro combinado) para mostrar el **Recordset** datos en una página Web.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="http://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>Comentarios  
 El identificador de clase para el **RDS. DataControl** objeto es BD96C556-65A3 - 11 D 0-983A-00C04FC29E33.  
  
> [!NOTE]
>  Si se produce un error que un [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) o **RDS. DataControl** objeto no carga, asegúrese de que está usando el identificador de clase correcto. La clase identificadores para estos objetos han cambiado desde la versión 1.0 y 1.1. Además, tener en cuenta que se deben establecer columnas admiten valores NULL incluso cuando se usa el **RDS DataControl** objeto.  
  
 En un escenario básico, debe establecer únicamente la **SQL**, **conectar**, y **Server** propiedades de la **RDS. DataControl** objeto, que llamará automáticamente el objeto comercial predeterminado, [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md).  
  
 Todas las propiedades de la **RDS. DataControl** son opcionales porque los objetos comerciales personalizados pueden reemplazar su funcionalidad.  
  
> [!NOTE]
>  Si utiliza una consulta para varios resultados, solo la primera [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) se devuelve. Si se necesitan varios conjuntos de resultados, asigne cada uno a su propio **DataControl**. Un ejemplo de una consulta para varios resultados podría ser la siguiente: `"Select * from Authors, Select * from Topics"`  
  
 Adición de "DFMode = 20;" a la cadena de conexión cuando se utiliza el **RDS. DataControl** objeto puede mejorar el rendimiento del servidor cuando se actualizan los datos. Con esta configuración, el **RDSServer.DataFactory** objeto en el servidor usa el modo de requiere menos recursos. Sin embargo, las siguientes características no están disponibles en esta configuración:  
  
-   Uso de consultas parametrizadas.  
  
-   Obtención de información de parámetro o columna antes de llamar a la **Execute** método.  
  
-   Establecer **Transact actualizaciones** a **True**.  
  
-   Obtener el estado de fila.  
  
-   Llamar a la [Resync](../../../ado/reference/ado-api/resync-method.md) método.  
  
-   Actualización (de forma explícita o automáticamente) a través de la [Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) propiedad.  
  
-   Establecer **comando** o [conjunto de registros](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) propiedades.  
  
-   Usar **adCmdTableDirect**.  
  
 El **RDS. DataControl** objeto se ejecuta en modo asincrónico de forma predeterminada. Si necesita una ejecución sincrónica para la aplicación, establezca el [ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md) igual al parámetro **adcExecSync** y [FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md) parámetro igual que **adcFetchUpFront**, tal y como se muestra en el ejemplo siguiente.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="http://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 Utilice uno **RDS. DataControl** objeto que se va a vincular los resultados de una sola consulta a uno o varios controles visuales. Por ejemplo, suponga que codifica una consulta solicita datos de cliente como nombre, domicilio, lugar de nacimiento, edad y estado de prioridad. Puede usar una sola **RDS. DataControl** objeto para mostrar el nombre, la edad y la región de un cliente en tres cuadros de texto independiente; Estado de prioridad en una casilla de verificación; y todos los datos de un control de cuadrícula.  
  
 Usar diferentes **RDS. DataControl** objetos para vincular los resultados de varias consultas a controles visuales diferentes. Por ejemplo, suponga que utiliza una consulta para obtener información acerca de un cliente y una segunda consulta para obtener información sobre los productos que el cliente ha adquirido. Desea mostrar los resultados de la primera consulta en tres cuadros de texto y una casilla de verificación y los resultados de la segunda consulta en un control de cuadrícula. Si utiliza el objeto de negocio predeterminado (**RDSServer.DataFactory**), debe hacer lo siguiente:  
  
-   Agregar dos **RDS. DataControl** objetos a la página Web.  
  
-   Escribir dos consultas, una para cada **SQL** propiedad de los dos **RDS. DataControl** objetos. Una **RDS. DataControl** objeto contendrá una consulta SQL que se solicita información del cliente; el segundo contendrá una consulta que solicita una lista de mercancía el cliente ha adquirido.  
  
-   En las etiquetas de objeto de todos los controles enlazados, especifique el valor DATAFLD para establecer los valores de los datos que desea mostrar en cada control visual.  
  
 No hay ninguna restricción de recuento del número de **RDS. DataControl** objetos que puede incrustar mediante etiquetas de objeto en una sola página Web.  
  
 Al definir la **RDS. DataControl** objeto en una página Web, utilice es distinto de cero **alto** y **ancho** valores como 1 (para evitar la inclusión de espacio adicional).  
  
 Componentes de cliente de servicio de datos remotos ya están incluidos como parte de Internet Explorer 4.0; por lo tanto, no es necesario incluir un parámetro CODEBASE en su **RDS. DataControl** etiqueta de objeto.  
  
 Con Internet Explorer 4.0 o posterior, puede enlazar a datos mediante controles HTML y ActiveX® solo si están marcados como controles de modelo de apartamento.  
  
> [!NOTE]
>  **Los usuarios de Microsoft Visual Basic** el **RDS. DataControl** es seguro para scripting y solo se usa en aplicaciones basadas en Web. Una aplicación de cliente de Visual Basic no tiene lo necesita.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del objeto DataControl (VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)






















