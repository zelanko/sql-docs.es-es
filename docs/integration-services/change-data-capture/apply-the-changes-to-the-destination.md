---
title: Aplicar los cambios al destino | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],applying changes
ms.assetid: 338a56db-cb14-4784-a692-468eabd30f41
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: db439c34845dc01c54752e01428fa9793f994fdb
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65729093"
---
# <a name="apply-the-changes-to-the-destination"></a>Aplicar los cambios al destino

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  En el flujo de datos de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que realiza una carga incremental de datos modificados, la tercera y última tarea consiste en aplicar los cambios al destino. Necesitará un componente para aplicar las inserciones, otro para aplicar las actualizaciones y otro más para aplicar las eliminaciones.  
  
> [!NOTE]  
>  La segunda tarea para diseñar el flujo de datos de un paquete que realiza una carga incremental de datos modificados consiste en separar las inserciones, las actualizaciones y las eliminaciones. Para obtener más información sobre este componente, vea [Procesar inserciones, actualizaciones y eliminaciones](../../integration-services/change-data-capture/process-inserts-updates-and-deletes.md). Para obtener una descripción del proceso general de creación de un paquete que realiza una carga incremental de los datos modificados, vea [Captura de datos modificados &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md).  
  
## <a name="applying-inserts"></a>Aplicar las inserciones  
 Para aplicar las inserciones, utilice un destino de OLE DB, ya que las nuevas filas no requieren ningún tratamiento especial.  
  
#### <a name="to-process-inserts-by-using-an-ole-db-destination"></a>Para procesar las inserciones mediante un destino de OLE DB  
  
1.  En la pestaña **Flujo de datos** , agregue un destino de OLE DB.  
  
2.  Conecte la salida que contiene las inserciones de la transformación División condicional al destino de OLE DB.  
  
3.  En el **Editor de destino de OLE DB**, en la página **Administrador de conexiones** , seleccione las opciones siguientes:  
  
    1.  Seleccione o cree un administrador de conexiones OLE DB para la base de datos de destino.  
  
    2.  Seleccione una opción de **Modo de acceso a datos** y, a continuación, seleccione la tabla de destino o escriba una instrucción SQL que contenga las columnas de destino.  
  
4.  En la página **Asignaciones** del editor, asigne las columnas apropiadas de los datos modificados a la tabla de destino.  
  
## <a name="applying-updates"></a>Aplicar las actualizaciones  
 Para aplicar las actualizaciones, utilice una transformación Comando de OLE DB. La razón para usar esta transformación es que hay que utilizar una instrucción UPDATE con parámetros para actualizar las filas de una en una con los nuevos valores de las columnas.  
  
> [!NOTE]  
>  También puede utilizar los componentes de destino para aplicar las actualizaciones. Al emplear este método, se usan los componentes de destino para guardar las filas en tablas temporales que se crean para este propósito. Después, se usan las tareas Ejecutar SQL para realizar operaciones de actualización y eliminación masivas con el destino a partir de las tablas temporales.  
  
#### <a name="to-process-updates-by-using-an-ole-db-command-transformation"></a>Para procesar las actualizaciones mediante una transformación Comando de OLE DB  
  
1.  En la pestaña **Flujo de datos** , agregue una transformación Comando de OLE DB.  
  
2.  Conecte la salida que contiene las actualizaciones de la transformación División condicional a la transformación Comando de OLE DB.  
  
3.  En la pestaña **Editor avanzado para Comando de OLE DB**, en la pestaña **Administrador de conexiones** , seleccione o cree un administrador de conexiones de OLE DB para la base de datos de destino.  
  
4.  En el **Editor avanzado para Comando de OLE DB**, en la pestaña **Propiedades de componente** , escriba una instrucción UPDATE con parámetros para **SqlCommand**.  
  
     Por ejemplo, una instrucción UPDATE para una tabla de clientes podría tener la sintaxis siguiente:  
  
    ```sql
    update CDCSample.Customer  
    set TerritoryID  = ?,  
        CustomerType  = ?,  
        rowguid  = ?,  
        ModifiedDate  = ?  
    where CustomerID = ?  
  
    ```  
  
5.  En la pestaña **Asignaciones de columnas** del editor, asigne las columnas apropiadas de los datos modificados a los parámetros de la instrucción UPDATE.  
  
## <a name="applying-deletes"></a>Aplicar las eliminaciones  
 Para aplicar las eliminaciones, utilice una transformación Comando de OLE DB. La razón para usar esta transformación es que hay que utilizar una instrucción DELETE con parámetros que elimina las filas de una en una basándose en el valor de columna que identifica la fila de forma exclusiva.  
  
> [!NOTE]  
>  También puede utilizar los componentes de destino para aplicar las eliminaciones. Al emplear este método, se usan los componentes de destino para guardar las filas en tablas temporales que se crean para este propósito. Después, se usan las tareas Ejecutar SQL para realizar operaciones de actualización y eliminación masivas con el destino a partir de las tablas temporales.  
  
#### <a name="to-process-deletes-by-using-an-ole-db-command-transformation"></a>Para procesar las eliminaciones mediante una transformación Comando de OLE DB  
  
1.  En la pestaña **Flujo de datos** , agregue una transformación Comando de OLE DB al flujo de datos.  
  
2.  Conecte la salida que contiene las eliminaciones de la transformación División condicional a la transformación Comando de OLE DB.  
  
3.  Abra el Editor avanzado para configurar la transformación.  
  
4.  En la pestaña **Editor avanzado para Comando de OLE DB**, en la pestaña **Administrador de conexiones** , seleccione o cree un administrador de conexiones de OLE DB para la base de datos de destino.  
  
5.  En el **Editor avanzado para Comando de OLE DB**, en la pestaña **Propiedades de componente** , escriba una instrucción DELETE con parámetros para **SqlCommand**.  
  
     Por ejemplo, una instrucción DELETE para una tabla de clientes podría tener la sintaxis siguiente:  
  
    ```sql
    delete from Customer where CustomerID = ?  
  
    ```  
  
6.  En la pestaña **Asignaciones de columnas** del editor, asigne la columna apropiada de los datos modificados al parámetro de la instrucción DELETE.  
  
## <a name="optimizing-inserts-and-updates-by-using-merge-functionality"></a>Optimizar inserciones y actualizaciones mediante la funcionalidad MERGE  
 Puede optimizar el procesamiento de inserciones y actualizaciones si combina ciertas opciones de captura de datos modificados con el uso de la palabra clave MERGE de Transact-SQL. Para obtener más información sobre la palabra clave MERGE, vea [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md).  
  
 En la instrucción Transact-SQL que recupera los datos modificados, puede especificar *all with merge* como el valor del parámetro *row_filter_option* al llamar a la función **cdc.fn_cdc_get_net_changes_<capture_instance>**. Esta función de captura de datos modificados funciona con más eficacia cuando no tiene que realizar el procesamiento adicional necesario para distinguir las inserciones de las actualizaciones. Al especificar el valor del parámetro *all with merge* , el valor **__$operation** de los datos modificados es 1 para las eliminaciones o 5 para los cambios producidos por las inserciones o actualizaciones. Para obtener más información sobre la función de Transact-SQL que se ha usado para recuperar los datos modificados, vea [Recuperar y describir datos modificados](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md). Una vez recuperados los cambios con el valor del parámetro *all with merge* , podrá aplicar las eliminaciones y almacenar las filas restantes en una tabla temporal o de ensayo. A continuación, en una tarea Ejecutar SQL de nivel inferior, puede utilizar una única instrucción MERGE para aplicar al destino todas las inserciones o actualizaciones de la tabla de ensayo.  
  
  
