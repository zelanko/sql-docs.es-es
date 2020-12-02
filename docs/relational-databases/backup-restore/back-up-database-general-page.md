---
title: Copia de seguridad de base de datos (página General) | Microsoft Docs
description: En SQL Server, use la página General del cuadro de diálogo Copia de seguridad de base de datos para ver o modificar la configuración de origen y destino de una operación de copia de seguridad de la base de datos.
ms.custom: ''
ms.date: 07/01/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.backupdatabase.general.f1
ms.assetid: 5c344dfd-1ad3-41cc-98cd-732973b4a162
author: cawrites
ms.author: chadam
ms.openlocfilehash: dd1dd775aff0865b2ce0f2f833ef78b7c5eb4b5e
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130577"
---
# <a name="back-up-database-general-page"></a>Copia de seguridad de base de datos (página General)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Utilice la página **General** del cuadro de diálogo **Copia de seguridad de base de datos** para ver o modificar la configuración de una operación de copia de seguridad de la base de datos.  
  
 Para obtener más información sobre los conceptos básicos de copias de seguridad, vea [Información general de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
> [!NOTE]  
>  Cuando especifica una tarea de copia de seguridad con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puede generar el script [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) correspondiente si hace clic en el botón **Script** y luego selecciona un destino para el script.  
  
 **Para utilizar SQL Server Management Studio a fin de crear una copia de seguridad**  
  
-   [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
    > [!IMPORTANT]  
    >  Puede definir un plan de mantenimiento de base de datos para crear copias de seguridad. Para obtener más información, vea [Planes de mantenimiento](../maintenance-plans/maintenance-plans.md) en los Libros en pantalla de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
 **Para crear una copia de seguridad parcial**  
  
-   En el caso de una copia de seguridad parcial, debe usar la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) con la opción PARTIAL.  
  
## <a name="options"></a>Opciones  
  
### <a name="source"></a>Source  
 Las opciones del panel **Origen** identifican la base de datos y especifican el tipo de copia de seguridad y el componente para la operación de copia de seguridad.  
  
 **Base de datos**  
 Seleccione la base de datos de la que desea hacer una copia de seguridad.  
  
 **Modelo de recuperación**  
 Vea el modelo de recuperación (SIMPLE, FULL o BULK_LOGGED) para la base de datos seleccionada.  
  
 **Tipo de copia de seguridad**  
 Seleccione el tipo de copia de seguridad que desea realizar para la base de datos especificada.  
  
|Tipo de copia de seguridad|Disponible para|Restricciones|  
|-----------------|-------------------|------------------|  
|Completo|Bases de datos, archivos y grupos de archivos|En la base de datos **maestra** , solo son posibles copias de seguridad completas.<br /><br /> En el modelo de recuperación simple, las copias de seguridad de archivos y grupos de archivos solo están disponibles para los grupos de archivos de solo lectura.|  
|Diferencial|Bases de datos, archivos y grupos de archivos|En el modelo de recuperación simple, las copias de seguridad de archivos y grupos de archivos solo están disponibles para los grupos de archivos de solo lectura.|  
|Registro de transacciones|Registros de transacciones|Las copias de seguridad de registros de transacciones no están disponibles para el modelo de recuperación simple.|  
  
 **Copia de seguridad de solo copia**  
 Seleccione esta opción para crear una copia de seguridad de solo copia. Una *copia de seguridad de solo copia* es una copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] independiente de la secuencia de copias de seguridad convencionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Copias de seguridad de solo copia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
> [!NOTE]  
>  Cuando la opción **Diferencial** está seleccionada, no puede crear una copia de seguridad de solo copia.  
  
 **Componente de copia de seguridad**  
 Seleccione el componente de la base de datos del que desea hacer una copia de seguridad. Si se selecciona **Registro de transacciones** en la lista **Tipo de copia de seguridad** , esta opción no estará activada.  
  
 Seleccione uno de los siguientes botones:  
  
|||  
|-|-|  
|**Base de datos**|Especifica que se realizará una copia de seguridad de toda la base de datos.|  
|**Archivos y grupos de archivos**|Especifica que se realizará una copia de seguridad de los archivos y grupos de archivos indicados.<br /><br /> Al seleccionar esta opción, se abre el cuadro de diálogo **Seleccionar archivos y grupos de archivos** . Después de seleccionar los grupos de archivos o los archivos que quiere incluir en la copia de seguridad y hacer clic en **Aceptar**, las selecciones aparecen en el cuadro **Archivos y grupos de archivos** .|  
  
### <a name="destination"></a>Destination  
 Las opciones del panel **Destino** permiten especificar el tipo de dispositivo de copia de seguridad para la operación de copia de seguridad y buscar un dispositivo de copia de seguridad lógico o físico existente.  
  
> [!NOTE]  
>  Para obtener más información sobre los dispositivos de copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 **Copia de seguridad en**  
 Seleccione uno de los siguientes tipos de medios en los que se hará la copia de seguridad. Los destinos que seleccione aparecerán en la lista **Copia de seguridad en** .  
  
|||  
|-|-|  
|**Disco**|Hace la copia de seguridad en disco. Puede tratarse de un archivo de sistema o un dispositivo de copia de seguridad basado en disco creado para la base de datos. Los discos seleccionados actualmente aparecerán en la lista **Copia de seguridad en** . Puede seleccionar hasta 64 dispositivos de disco para la operación de copia de seguridad.|  
|**Cinta**|Hace la copia de seguridad en cinta. Puede tratarse de una unidad de cinta local o un dispositivo de copia de seguridad basado en cinta creado para la base de datos. Las cintas seleccionadas actualmente aparecerán en la lista **Copia de seguridad en** . El número máximo es 64. Si no hay dispositivos de cinta conectados al servidor, esta opción no estará activada. Las cintas que seleccione aparecerán en la lista **Copia de seguridad en** .<br /><br /> Nota: La compatibilidad con dispositivos de cinta de copia de seguridad se quitará en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.|  
|**URL**|Hace la copia de seguridad del almacenamiento de blobs de Microsoft Azure.|  
  
 El siguiente conjunto de las opciones que aparecen depende del tipo de destino seleccionado. Si selecciona Disco o Cinta, se muestran las siguientes opciones.  
  
 **Add (Agregar)**  
 Agrega un archivo o un dispositivo a la lista **Copia de seguridad en** . Puede hacer copias de seguridad de hasta 64 dispositivos simultáneamente en un disco remoto o local. Para especificar un archivo en un disco remoto, utilice el nombre UNC (convención de nomenclatura universal) completo. Para obtener más información, vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
 
 
  
 **Remove**  
 Quita uno o más dispositivos seleccionados actualmente de la lista **Copia de seguridad en** .  
  
 **Contents**  
Muestra el contenido del medio del dispositivo seleccionado, si existe.  El botón no realiza una función cuando se especifica una dirección **URL** . 
   
Cuadro de diálogo **Seleccionar destino de la copia de seguridad** . El cuadro de diálogo **Seleccionar destino de la copia de seguridad** aparece después de seleccionar **Agregar**.   El conjunto de las opciones que aparecen depende del tipo de destino seleccionado. 

Si ha seleccionado **Disco** o **Cinta** como el destino de la copia de seguridad, se muestra la siguiente opción.  

*
  **Nombre de archivo**  
    Especifica el nombre del archivo de copia de seguridad.

Si ha seleccionado la dirección **URL** como el destino de la copia de seguridad, se muestran las siguientes opciones:
*
  **Contenedor de almacenamiento de Windows Azure**  
  El nombre del contenedor de almacenamiento de Microsoft Azure para almacenar los archivos de copia de seguridad. 
   
*
  **Directiva de acceso compartido:**  
  Especifique la firma de acceso compartido para un contenedor especificado manualmente.  Este campo no está disponible si se ha elegido un contenedor existente.
  
*
  **Archivo de copia de seguridad:**  
  Nombre del archivo de copia de seguridad.

*
  **Nuevo contenedor:**  
Se usa para registrar un contenedor existente para el que no tiene una firma de acceso compartido.  Vea [Connect to a Microsoft Azure Subscription (Conectarse a una suscripción de Microsoft Azure)](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md).
  
## <a name="see-also"></a>Consulte también  
 [Realizar copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [Realizar copias de seguridad de archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Definir un dispositivo lógico de copia de seguridad para un archivo de disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [Definir un dispositivo lógico de copia de seguridad en una unidad de cinta &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  
