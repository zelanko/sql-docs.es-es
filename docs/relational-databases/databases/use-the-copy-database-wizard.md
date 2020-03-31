---
title: Usar el Asistente para copiar bases de datos | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.cdw.packageconfiguration.f1
- sql13.swb.cdw.schedule.f1
- sql13.swb.cdw.transfermethod.f1
- sql13.swb.cdw.databases.f1
- sql13.swb.cdw.destinationconfiguration.f1
- sql13.swb.cdw.destination.f1
- sql13.swb.cdw.locationofsourcedbfiles.f1
- sql13.swb.cdw.source.f1
- sql13.swb.cdw.selectdatabaseobjects.f1
- sql13.swb.cdw.complete.f1
- sql13.swb.cdw.welcome.f1
helpviewer_keywords:
- Copy Database Wizard
- starting Copy Database Wizard
ms.assetid: 7a999fc7-0a26-4a0d-9eeb-db6fc794f3cb
author: stevestein
ms.author: sstein
ms.openlocfilehash: 67488a92a14a2533c9ba6ef14941b11b8bcbb8c2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68127115"
---
# <a name="use-the-copy-database-wizard"></a>Usar el Asistente para copiar bases de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
El Asistente para copiar bases de datos permite mover o copiar bases de datos y determinados objetos de servidor de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  a otra fácilmente, sin tiempo de inactividad del servidor. Mediante este asistente, puede hacer lo siguiente: 
  
-   Elegir un servidor de origen y de destino  
  
-   Seleccionar las bases de datos que se van a mover o copiar.  
  
-   Especificar la ubicación del archivo de las bases de datos.  
  
-   Copiar inicios de sesión en el servidor de destino.  
  
-   Copiar otros objetos de ayuda, trabajos, mensajes de error y procedimientos almacenados definidos por el usuario.  
  
-   Programar cuándo mover o copiar las bases de datos.  
  

##  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El Asistente para copiar bases de datos no está disponible en la edición Express.  
  
-   El Asistente para copiar bases de datos no se puede usar para copiar o mover bases de datos que:
  
    -   Se encuentren en el sistema.
  
    -   Estén marcadas para la replicación.
  
    -   Estén marcadas como no accesibles, en carga, sin conexión, en recuperación, sospechosas o en modo de emergencia.
    
    -   Tengan archivos de registro o datos almacenados en el almacenamiento de Microsoft Azure.
  
-   Cuando se usa [FileTables](../../relational-databases/blob/filetables-sql-server.md), no se puede utilizar el Asistente para copiar bases de datos en el mismo servidor, ya que el asistente usa el mismo nombre de directorio.

-   Una base de datos no se puede mover ni copiar a una versión anterior de SQL Server.
  
-   Si selecciona la opción **Mover** , el asistente elimina automáticamente la base de datos de origen después de moverla. El Asistente para copiar bases de datos no elimina una base de datos de origen si se selecciona la opción **Copiar** .  Además, los objetos de servidor seleccionados se copian en lugar de moverse al destino; la base de datos es el único objeto que realmente se mueve.
  
-   Si usa el método de objeto de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para mover el catálogo de texto completo, debe volver a rellenar el índice después del movimiento.  
  
-   El método de **separar y adjuntar** separa la base de datos, mueve o copia los archivos .mdf, .ndf y .ldf de la base de datos y vuelve a adjuntar la base de datos en la nueva ubicación. En el método de **separar y adjuntar** , para evitar la incoherencia o la pérdida de datos, las sesiones activas no pueden adjuntarse a la base de datos que se va a copiar o mover. En el método de objeto de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se permiten las sesiones activas porque la base de datos nunca está sin conexión.  

-    Transferir trabajos del Agente SQL Server que hacen referencia a bases de datos que todavía no existen en el servidor de destino producirá un error en toda la operación.  El Asistente intenta crear un trabajo del Agente SQL Server antes de crear la base de datos.  Solución alternativa:
     1. Cree una base de datos de shell en el servidor de destino con el mismo nombre que el de la base de datos que se va a copiar o mover.  Vea [Crear una base de datos](../../relational-databases/databases/create-a-database.md).
     
     2. De la página **Configurar base de datos de destino** , seleccione **Quitar cualquier base de datos del servidor de destino que tenga el mismo nombre y continuar con la transferencia (sobrescribiendo los archivos de base de datos existentes)** .

> **IMPORTANTE:** El método de **separar y adjuntar** hará que la propiedad de base de datos de origen y de destino llegue a establecerse en el inicio de sesión que ejecuta el **Asistente para copiar bases de datos**.  Vea [ALTER AUTHORIZATION (Transact-SQL)](../../t-sql/statements/alter-authorization-transact-sql.md) para cambiar la propiedad de una base de datos.
  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> Requisitos previos  
-   Asegúrese de que el Agente SQL Server se inició en el servidor de destino.  

-   Asegúrese de que se pueda acceder a los directorios de archivo de registro y datos en el servidor de origen desde el servidor de destino.

-   En el método de **separar y adjuntar** , un proxy del Agente SQL Server del subsistema de SSIS debe existir en el servidor de destino con una credencial que pueda tener acceso al sistema de archivos de los servidores de origen y de destino. Para obtener más información sobre los servidores proxy, vea [Crear un proxy del Agente SQL Server](~/ssms/agent/create-a-sql-server-agent-proxy.md).

> **IMPORTANTE:** En el método de **separar y adjuntar** , el proceso de copiar o mover producirá un error si no se usa una cuenta de proxy de Integration Services.  En determinadas situaciones, la base de datos de origen no se volverá a adjuntar al servidor de origen y todos los permisos de seguridad NTFS se quitarán de los archivos de registro y datos.  Si esto sucede, vaya a sus archivos, vuelva a aplicar los permisos relevantes y, después, vuelva a adjuntar la base de datos a su instancia de SQL Server.
  
##  <a name="recommendations"></a><a name="Recommendations"></a> Recomendaciones  
  
-   Para asegurarse del rendimiento óptimo de una base de datos actualizada, ejecute [sp_updatestats (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md) (actualizar estadísticas) en la base de datos actualizada.  
  
-   Al mover o copiar una base de datos a otra instancia de servidor, para proporcionar una experiencia coherente a los usuarios y las aplicaciones, puede que tenga que volver a crear algunos o todos los metadatos de la base de datos, por ejemplo los inicios de sesión y los trabajos, en la otra instancia de servidor. Para obtener más información, vea [Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia del servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  

  
###  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Debe ser miembro del rol fijo de servidor **sysadmin** tanto en el servidor de origen como en el servidor de destino.  
  
##  <a name="the-copy-database-wizard-pages"></a><a name="Overview"></a> Las páginas del Asistente para copiar bases de datos 
Inicie el **Asistente para copiar bases de datos** en SQL Server Management Studio desde el **Explorador de objetos** y expanda **Bases de datos**.  Después, haga clic con el botón derecho en una base de datos, seleccione **Tareas**y, luego, haga clic en **Copiar base de datos**.  Si aparece la página inicial **Asistente para copiar bases de datos** , haga clic en **Siguiente**.


### <a name="select-a-source-server"></a>Seleccionar un servidor de origen
Se usa para especificar el servidor donde se encuentra la base de datos que se va a mover o copiar, y para escribir la información de inicio de sesión.  Después de seleccionar el método de autenticación y especificar la información de inicio de sesión, haga clic en **Siguiente** para establecer la conexión al servidor de origen.  Esta conexión permanece abierta durante toda la sesión.

-    **Servidor de origen**  
Se usa para identificar el nombre del servidor en el que se encuentran las bases de datos que quiere mover o copiar.  Escriba manualmente o haga clic en los puntos suspensivos para dirigirse al servidor deseado.  La versión del servidor debe ser, por lo menos, SQL Server 2005.

-    **Utilizar autenticación de Windows**  
Permite que un usuario se conecte a través de una cuenta de usuario de Microsoft Windows.

-    **Utilizar autenticación de SQL Server**  
Permite que un usuario se conecte proporcionando el nombre de usuario y la contraseña de autenticación de SQL Server.

     -    **Nombre de usuario**  
Se usa para escribir el nombre de usuario con el que se va a conectar. Esta opción solo está disponible si ha seleccionado la **autenticación de SQL Server**para conectarse.

     -    **Contraseña**  
Se usa para escribir la contraseña del inicio de sesión. Esta opción solo está disponible si ha seleccionado la **autenticación de SQL Server**para conectarse.

###  <a name="select-a-destination-server"></a>Seleccionar un servidor de destino
Se usa para especificar el servidor al que se moverá o se copiará la base de datos.  Si establece los servidores de origen y de destino en la misma instancia de servidor, realizará una copia de la base de datos.  En este caso, debe cambiar el nombre de la base de datos posteriormente en el asistente.  Puede usarse el nombre de la base de datos de origen para la base de datos copiada o movida únicamente si no existe algún conflicto de nombres en el servidor de destino.  Si existe algún conflicto de nombre, debe solucionarse manualmente en el servidor de destino antes de poder utilizar el nombre de la base de datos de origen.
  
-    **Servidor de destino**  
Se usa para identificar el nombre del servidor en el que se encuentran las bases de datos que quiere mover o copiar.  Escriba manualmente o haga clic en los puntos suspensivos para dirigirse al servidor deseado.  La versión del servidor debe ser, por lo menos, SQL Server 2005.

     >**NOTA** Puede usar un destino que sea un servidor en clúster; el Asistente para copiar bases de datos se asegurará de que solo se seleccionen unidades compartidas en un servidor de destino en clúster.

-    **Utilizar autenticación de Windows**  
Permite que un usuario se conecte a través de una cuenta de usuario de Microsoft Windows.

-    **Utilizar autenticación de SQL Server**  
Permite que un usuario se conecte proporcionando el nombre de usuario y la contraseña de autenticación de SQL Server.

     -    **Nombre de usuario**  
Se usa para escribir el nombre de usuario con el que se va a conectar. Esta opción solo está disponible si ha seleccionado la **autenticación de SQL Server**para conectarse.

     -    **Contraseña**  
Se usa para escribir la contraseña del inicio de sesión. Esta opción solo está disponible si ha seleccionado la **autenticación de SQL Server**para conectarse.

###  <a name="select-the-transfer-method"></a>Seleccionar el método de transferencia
 
-    **Usar el método de separar y adjuntar**  
Esta opción separa la base de datos del servidor de origen, copia los archivos de base de datos (.mdf, .ndf y .ldf) al servidor de destino y adjunta la base de datos al servidor de destino. Generalmente, este método es el más rápido, ya que la tarea principal consiste en leer el disco de origen y escribir en el disco de destino. No se necesita lógica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para crear objetos en la base de datos ni para crear estructuras de almacenamiento de datos. Sin embargo, este método puede ser más lento si la base de datos contiene una gran cantidad de espacio asignado, pero sin utilizar. Por ejemplo, una nueva base de datos casi vacía que se crea con una asignación de 100 MB, copia los 100 MB, aunque solo se utilicen 5 MB.

     > **NOTA** Este método impide que la base de datos esté disponible para los usuarios durante la transferencia.

     -    **Si se produce un error, volver a adjuntar la base de datos de origen**  
     Cuando se copia una base de datos, los archivos originales de la base de datos siempre se vuelven a adjuntar al servidor de origen. Utilice este cuadro para volver a adjuntar los archivos originales a la base de datos de origen si no se puede mover una base de datos. 
  
-    **Usar el método de objeto de administración de SQL**  
     Este método lee la definición de cada objeto de la base de datos de origen y lo crea en la base de datos de destino. A continuación, transfiere los datos de las tablas de origen a las tablas de destino y vuelve a crear los índices y metadatos.
  
     > [!NOTE]
     >  Los usuarios de la base de datos pueden tener acceso a ella durante la transferencia. 
  
###  <a name="select-database"></a>Seleccionar base de datos
Seleccione las bases de datos que quiere mover o copiar del servidor de origen al servidor de destino.  Consulte [Limitaciones y restricciones](#Restrictions) en la parte superior del tema.  
  
-    **Mover**  
Seleccione esta opción para mover la base de datos al servidor de destino.

-    **Copy**  
Seleccione esta opción para copiar la base de datos al servidor de destino.

-    **Origen**  
Muestra las bases de datos que hay en el servidor de origen.

-    **Estado**  
Muestra información diversa de la base de datos de origen.

-    **Actualizar**  
Actualiza la lista de bases de datos.
  
### <a name="configure-destination-database"></a>Configurar base de datos de destino
Cambie el nombre de la base de datos si es adecuado y especifique la ubicación y los nombres de los archivos de base de datos.  Esta página aparecerá una vez para cada base de datos que se mueva o se copie.

-    **Base de datos de origen**  
Nombre de la base de datos de origen.  El cuadro de texto no es editable.

-    **Base de datos de destino**  
El nombre de la base de datos de destino que se va a crear. Puede modificarlo como quiera.

-    **Archivos de la base de datos de destino:**  
     
     -    **Nombre de archivo**  
El nombre del archivo de base de datos de destino que se va a crear. Puede modificarlo como quiera.

     -    **Tamaño (MB)**  
El tamaño del archivo de base de datos de destino en megabytes.

     -    **Carpeta de destino**  
La carpeta del servidor de destino que va a hospedar el archivo de base de datos de destino. Puede modificarla como quiera.

     -    **Estado**  
Status

-    **Si la base de datos de destino ya existe:**  
     Decida qué acción realizar si la base de datos de destino ya existe.

     -    **Detener la transferencia si existe una base de datos o un archivo con el mismo nombre en el destino.**

     -    **Quitar cualquier base de datos del servidor de destino que tenga el mismo nombre y continuar con la transferencia (sobrescribiendo los archivos de base de datos existentes).**

###  <a name="select-server-objects"></a>Seleccionar los objetos de servidor 
Esta página solo está disponible cuando el origen y el destino están en servidores diferentes.  
  
-    **Objetos relacionados disponibles**  
Enumera los objetos disponibles que se van a transferir al servidor de destino.  Para incluir un objeto, haga clic en el nombre del objeto en el cuadro **Objetos relacionados disponibles** y, después, haga clic en el botón **>>** para mover el objeto al cuadro **Objetos relacionados seleccionados** . 

-    **Objetos relacionados seleccionados**  
Enumera los objetos que se transferirán al servidor de destino.  Para excluir un objeto, haga clic en el nombre del objeto en el cuadro **Objetos relacionados seleccionados** y, después, haga clic en el botón **<\<** para mover el objeto al cuadro **Objetos relacionados disponibles** .  De forma predeterminada, se transfieren todos los objetos de cada tipo seleccionado. Para elegir objetos individuales de cualquier tipo, haga clic en el botón de puntos suspensivos situado junto a cualquier tipo de objeto en el cuadro **Objetos relacionados seleccionados** .  Se abrirá un cuadro de diálogo en el que podrá seleccionar objetos individuales.

-    **Lista de objetos de servidor** 

      -    **Inicios de sesión (Esta opción está seleccionada de manera predeterminada).** 
  
     -    **trabajos del Agente SQL Server**  
  
     -    **Mensajes de error definidos por el usuario**  
  
     -    **Extremos**  
  
     -    **Catálogo de texto completo** 
  
     -    **Paquete SSIS**  
     
     -    **Procedimientos almacenados de la base de datos maestra** 
          >**NOTA** No se pueden elegir procedimientos almacenados extendidos y sus DLL asociadas para realizar copias automáticas.  
    
  
###   <a name="location-of-source-database-files"></a>Ubicación de los archivos de base de datos de origen
Esta página solo está disponible cuando el origen y el destino están en servidores diferentes.  Especifique un recurso compartido del sistema de archivos que contenga los archivos de base de datos del servidor de origen.
  
-    **Base de datos**  
     Muestra el nombre de las bases de datos que se mueven.  
  
-    **Ubicación de la carpeta**  
La ubicación de la carpeta de los archivos de base de datos en el servidor de origen.
Por ejemplo: `C:\Program Files\Microsoft SQL Server\MSSQL110.MSSQLSERVER\MSSQL\DATA`.

  
-    **Recurso compartido de archivos en el servidor de origen**  
El recurso compartido de archivos que contiene los archivos de base de datos en el servidor de origen.  Escriba manualmente el recurso compartido o haga clic en los puntos suspensivos para dirigirse a este.
Por ejemplo: `\\server_name\C$\Program Files\Microsoft SQL Server\MSSQL110.MSSQLSERVER\MSSQL\Data`.

### <a name="configure-the-package"></a>Configurar el paquete
El Asistente para copiar bases de datos crea un paquete SSIS para transferir la base de datos.

-    **Ubicación del paquete**  
Muestra el lugar donde se escribirá el paquete SSIS.

-    **Nombre del paquete**  
Se creará un nombre predeterminado para el paquete SSIS. Puede modificarlo como quiera.

-    **Opciones de registro**  
Seleccione si desea almacenar la información de registro en un archivo de texto o en el registro de eventos de Windows.

-    **Ruta del archivo de registro de errores**  
Esta opción solo está disponible si está seleccionada la opción de registro del archivo de texto.  Proporcione una ruta de acceso para la ubicación del archivo de registro. 

### <a name="schedule-the-package"></a>Programar el paquete
Especifique cuándo quiere que se inicie la operación de mover o copiar.  Si no es administrador del sistema, debe especificar una cuenta de proxy del Agente SQL Server que tenga acceso al subsistema de ejecución de paquetes de Integration Services (SSIS).

> **IMPORTANTE:** Se debe usar una cuenta de proxy de Integration Services en el método de **separar y adjuntar** .  

-    **Run immediately**  
     El paquete SSIS se ejecutará después de completar el asistente.
  
-    **Programación**  
     El paquete SSIS se ejecutará de acuerdo a una programación. 
  
     -    **Cambiar programación**   
Se abre el cuadro de diálogo **Nueva programación de trabajo** .  Configúrela como quiera.  Haga clic en **Aceptar** cuando haya finalizado.


-    **Cuenta de proxy de Integration Services** Seleccione una cuenta de proxy disponible de la lista desplegable.  Para programar la transferencia, el usuario debe disponer al menos de una cuenta de proxy, configurada con permisos para el **Subsistema de ejecución de paquetes SSIS**.

        Para crear una cuenta de proxy para la ejecución de paquetes SSIS, en el **Explorador de objetos**, expanda **Agente SQL Server**, expanda **Servidores proxy**, haga clic con el botón derecho en **Ejecución de paquete SSIS**y, después, haga clic en **Nuevo proxy**.

### <a name="complete-the-wizard"></a>Finalizar el asistente
Muestra un resumen de las opciones seleccionadas.  Haga clic en **Atrás** para cambiar una opción.  Haga clic en **Finalizar** para crear el paquete SSIS. La página **Realizando operación** supervisa la información de estado sobre la ejecución del **Asistente para copiar bases de datos**.

-    **Acción**  
 Enumera cada acción que se está ejecutando.

-    **Estado**  
 Indica si la acción, en su conjunto, concluyó correctamente o no.

-    **Mensaje**  
Proporciona los mensajes devueltos en cada paso.

##  <a name="examples"></a><a name="Examples"></a> Ejemplos
### <a name="common-steps"></a>**Pasos comunes** 
Independientemente de si elige **Mover** o **Copiar**, **Separar y adjuntar** o **SMO**, los cinco pasos que se enumeran a continuación serán los mismos.  Por motivos de brevedad, los pasos se enumeran aquí una vez y todos los ejemplos se iniciarán en el **paso 6**.

1.  En el **Explorador de objetos**, conéctese a una instancia del Motor de base de datos de SQL Server y expándala.

2.  Expanda **Bases de datos**, haga clic con el botón derecho en la base de datos deseada, seleccione **Tareas**y, después, haga clic en **Copiar base de datos...** .

3.  Si aparece la página inicial **Asistente para copiar bases de datos** , haga clic en **Siguiente**.

4.  Página **Seleccionar un servidor de origen**: especifique el servidor con la base de datos que se va a mover o copiar.  Seleccione el método de autenticación.  Si se elige **Usar autenticación de SQL Server** , necesitará escribir las credenciales de inicio de sesión.  Haga clic en **Siguiente** para establecer la conexión al servidor de origen.  Esta conexión permanece abierta durante toda la sesión.

5.  Página **Seleccionar un servidor de destino**:  especifique el servidor al que se va a mover o copiar la base de datos.  Seleccione el método de autenticación.  Si se elige **Usar autenticación de SQL Server** , necesitará escribir las credenciales de inicio de sesión.  Haga clic en **Siguiente** para establecer la conexión al servidor de origen.  Esta conexión permanece abierta durante toda la sesión.

     > **NOTA** Puede iniciar el Asistente para copiar bases de datos desde cualquier base de datos.  Puede usar al Asistente para copiar bases de datos desde el servidor de origen o de destino.
  
### <a name="a--move-database-using-detach-and-attach-method-to-an-instance-on-a-different-physical-server--a-login-and-sql-server-agent-job-will-be-moved-as-well"></a>**A.  Mover bases de datos mediante el método de separar y adjuntar a una instancia en un servidor físico diferente.  También se moverá un inicio de sesión y el trabajo del Agente SQL Server.**  
En el siguiente ejemplo se moverá la base de datos `Sales` , un inicio de sesión de Windows denominado `contoso\Jennie` y un trabajo del Agente SQL Server denominado `Jennie's Report` de una instancia de SQL Server 2008 en `Server1` a una instancia de SQL Server 2016 en `Server2`.  `Jennie's Report` usa la base de datos `Sales` .  `Sales` no existe todavía en el servidor de destino, `Server2`.  `Server1` se volverá a asignar a un equipo diferente después del traslado de la base de datos.
  
6.  Como se ha indicado anteriormente en [Limitaciones y restricciones](#Restrictions), una base de datos de shell necesitará crearse en el servidor de destino al transferir un trabajo del Agente SQL Server que haga referencia a una base de datos que todavía no exista en el servidor de destino.  Cree una base de datos de shell denominada `Sales` en el servidor de destino. 

7.  De vuelta en el **asistente**, página **Seleccionar el método de transferencia**:  revise y mantenga los valores predeterminados.  Haga clic en **Next**.
  
8.  Página **Seleccionar bases de datos**: active la casilla **Mover** para la base de datos deseada, `Sales`.  Haga clic en **Next**.
  
9.  Página **Configurar base de datos de destino**:  el **Asistente** ha identificado que `Sales` ya existe en el servidor de destino, como se ha creado en el **paso 6** anterior, y ha anexado `_new` al nombre de la **base de datos de destino**.  Elimine `_new` del cuadro de texto **Base de datos de destino** .  Si quiere, puede cambiar el **nombre de archivo**y la **carpeta de destino**.  Seleccione **Quitar cualquier base de datos del servidor de destino que tenga el mismo nombre y continuar con la transferencia (sobrescribiendo los archivos de base de datos existentes)** .  Haga clic en **Next**.
  
10. Página **Seleccionar los objetos de servidor**: en el panel **Objetos relacionados seleccionados:** , haga clic en el botón de puntos suspensivos de **Object name Logins** (Inicios de sesión del nombre de objeto).  En **Opciones de copia** , seleccione **Copiar solo los inicios de sesión seleccionados:** .  Active el cuadro de **Mostrar todos los inicios de sesión del servidor**.  Active el cuadro de **Inicio de sesión** para `contoso\Jennie`.  Haga clic en **OK**.  En el panel **Objetos relacionados disponibles:** , seleccione **Trabajos del Agente SQL Server** y, después, haga clic en el botón **>** .  En el panel **Objetos relacionados seleccionados:** , haga clic en el botón de puntos suspensivos de **Trabajos del Agente SQL Server**.  En **Opciones de copia** , seleccione **Copiar solo los trabajos seleccionados:** .  Active el cuadro de `Jennie's Report`.  Haga clic en **OK**.  Haga clic en **Next**.  
  
11. Página **Ubicación de los archivos de base de datos de origen**:  haga clic en el botón de puntos suspensivos de **Recurso compartido de archivos en el servidor de origen** y vaya a la ubicación de la carpeta especificada.  Por ejemplo, la ubicación de la carpeta `D:\MSSQL13.MSSQLSERVER\MSSQL\DATA` usa `\\Server1\D$\MSSQL13.MSSQLSERVER\MSSQL\DATA` para **Recurso compartido de archivos en el servidor de origen**.  Haga clic en **Next**.
  
12. Página **Configurar el paquete**:  en el cuadro de texto **Nombre del paquete:** escriba `SalesFromServer1toServer2_Move`.  Active la casilla de **¿Quiere guardar registros de transferencia?** .  En la lista desplegable **Opciones de registro** , seleccione **Archivo de texto**.  Tenga en cuenta la **ruta del archivo de registro de errores**. Puede revisarla si quiere.  Haga clic en **Next**.  
  
     > **NOTA** La **ruta del archivo de registro de errores** es la ruta de acceso del servidor de destino.
  
13. Página **Programar el paquete**:  Seleccione el proxy correspondiente de la lista desplegable **Cuenta de proxy de Integration Services** .  Haga clic en **Next**.

14. Página **Finalización del asistente**:  revise el resumen de las opciones seleccionadas.  Haga clic en **Atrás** para cambiar una opción.  Haga clic en **Finalizar** para ejecutar la tarea.  Durante la transferencia, la página **Realizando operación** supervisa la información de estado sobre la ejecución del **Asistente**.

15. Página **Realizando operación**: si la operación es correcta, haga clic en **Cerrar**.  Si la operación no se ha realizado correctamente, revise el registro de errores y, posiblemente, vaya **Atrás** para una revisión posterior.  De otro modo, haga clic en **Cerrar**.
  
16. **Pasos posteriores del movimiento** Considere la posibilidad de ejecutar las siguientes instrucciones T-SQL en el nuevo host, `Server2`:
  
     ~~~ tsql 
     ALTER AUTHORIZATION ON DATABASE::Sales TO sa;

     ALTER DATABASE Sales 
     SET COMPATIBILITY_LEVEL = 130;

     USE Sales
     GO

     EXEC sp_updatestats;
     ~~~
 
17. **Limpieza de los pasos posteriores del movimiento**  
Como `Server1` se moverá a un equipo diferente y la operación **Mover** no se repetirá, considere la posibilidad de ejecutar los siguientes pasos:
     -    Eliminar el paquete SSIS `SalesFromServer1toServer2_Move` en `Server2`.
     -    Eliminar el trabajo del Agente SQL Server `SalesFromServer1toServer2_Move` en `Server2`.
     -    Eliminar el trabajo del Agente SQL Server `Jennie's Report` en `Server1`.
     -    Quitar el inicio de sesión `contoso\Jennie` en `Server1`.


### <a name="b-----copy-database-using-detach-and-attach-method-to-the-same-instance-and-set-recurring-schedule"></a>**B.     Copiar bases de datos mediante el método de separar y adjuntar a la misma instancia y establecer una programación periódica.**  
En este ejemplo, la base de datos `Sales` se copiará y creará como `SalesCopy` en la misma instancia.  Por lo tanto, `SalesCopy`se volverá a crear semanalmente.

6.  Página **Seleccionar el método de transferencia**:  revise y mantenga los valores predeterminados.  Haga clic en **Next**.

7.  Página **Seleccionar bases de datos**: active la casilla **Copiar** para la base de datos `Sales`.  Haga clic en **Next**.

8.  Página **Configurar base de datos de destino**: Cambie el nombre de la **base de datos de destino** por `SalesCopy`.  Si quiere, puede cambiar el **nombre de archivo**y la **carpeta de destino**.  Seleccione **Quitar cualquier base de datos del servidor de destino que tenga el mismo nombre y continuar con la transferencia (sobrescribiendo los archivos de base de datos existentes)** .  Haga clic en **Next**.

9.  Página **Configurar el paquete**:  en el cuadro de texto **Nombre del paquete:** escriba `SalesCopy Weekly Refresh`.  Active la casilla de **¿Quiere guardar registros de transferencia?** .  Haga clic en **Next**.

10. Página **Programar el paquete**:  haga clic en el botón de radio **Programación:** y, después, haga clic en el botón **Cambiar programación**. 
 
    1. Página **Nueva programación del trabajo**: en el cuadro de texto **Nombre** escriba `Weekly on Sunday`. 
          
    2. Haga clic en **OK**.

11. Seleccione el proxy correspondiente de la lista desplegable **Cuenta de proxy de Integration Services** .  Haga clic en **Next**.

12. Página **Finalización del asistente**:  revise el resumen de las opciones seleccionadas.  Haga clic en **Atrás** para cambiar una opción.  Haga clic en **Finalizar** para ejecutar la tarea.  Durante la creación del paquete, la página **Realizando operación** supervisa la información de estado sobre la ejecución del **Asistente**.

13. Página **Realizando operación**: si la operación es correcta, haga clic en **Cerrar**.  Si la operación no se ha realizado correctamente, revise el registro de errores y, posiblemente, vaya **Atrás** para una revisión posterior.  De otro modo, haga clic en **Cerrar**.

14. Iniciar manualmente el trabajo del Agente SQL Server `SalesCopy weekly refresh`recién creado.  Revise el historial de trabajos y asegúrese de que `SalesCopy` ahora existe en la instancia.

  
##  <a name="follow-up-after-upgrading-a-database"></a><a name="FollowUp"></a> Seguimiento: después de actualizar una base de datos  
 Después de usar el Asistente para actualizar una base de datos de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la base de datos está disponible inmediatamente y se actualiza de forma automática. Si la base de datos tiene índices de texto completo, el proceso de actualización los importa, los restablece o los vuelve a generar, en función del valor de la propiedad del servidor **Opción de actualización de texto completo** . Si la opción de actualización se establece en **Importar** o en **Volver a generar**, los índices de texto completo no estarán disponibles durante la actualización. Dependiendo de la cantidad de datos que se indicen, la importación puede requerir varias horas y volver a generar puede requerir hasta diez veces más. Tenga en cuenta también que si la opción de actualización se establece en **Importar**y no hay disponible ningún catálogo de texto completo, se vuelven a generar los índices de texto completo asociados. Para obtener más información sobre cómo ver o cambiar la configuración de la propiedad **Opción de actualización de texto completo** , vea [Administrar y supervisar la búsqueda de texto completo para una instancia de servidor](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md).  
  
 Si el nivel de compatibilidad de una base de datos de usuario era 100 o superior antes de la actualización, permanece igual después de la misma. Si el nivel de compatibilidad era 90 en la base de datos actualizada, el nivel de compatibilidad se establece en 100, que es el nivel de compatibilidad mínimo admitido en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
 
 ## <a name="post-copy-or-move-considerations"></a><a name="Post"></a> Consideraciones posteriores a la copia o el movimiento
 Considere la posibilidad de realizar los siguientes pasos después de una operación de **Copiar** o **Mover**:
-    Cambiar la propiedad de las bases de datos cuando se use el método de separar y adjuntar.
-    Quitar los objetos de servidor en el servidor de origen después de una operación de **Mover**.
-    Quitar el paquete SSIS que ha creado el Asistente en el servidor de destino.
-    Quitar el trabajo del Agente SQL Server que ha creado el Asistente en el servidor de destino.

  
## <a name="more-information"></a>Más información 
 [Actualizar una base de datos mediante Separar y Adjuntar &#40;Transact-SQL&#41;](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md)   
 [Crear un proxy del Agente SQL Server](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
  
  

