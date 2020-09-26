---
title: Configurar WSUS
description: Estas instrucciones le guiarán por los pasos necesarios para usar el Asistente para configuración de Windows Server Update Services (WSUS) para configurar WSUS para el sistema de plataforma de análisis.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6882700208e165464261f236cadd00b30503b81f
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379583"
---
# <a name="configure-windows-server-update-services-wsus-in-analytics-platform-system"></a>Configuración de Windows Server Update Services (WSUS) en Analytics Platform System
Estas instrucciones le guiarán por los pasos necesarios para usar el Asistente para configuración de Windows Server Update Services (WSUS) para configurar WSUS para el sistema de plataforma de análisis. Debe configurar WSUS para poder aplicar actualizaciones de software al dispositivo. WSUS ya está instalado en la máquina virtual de VMM del dispositivo.  
  
Para obtener más información acerca de la configuración de WSUS, consulte la [Guía de instalación paso a paso de WSUS](/windows/deployment/deploy-whats-new) en el sitio web de WSUS. Después de configurar WSUS, consulte [Descargar y aplicar actualizaciones de Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md) para iniciar una actualización.  
  
> [!WARNING]  
> Si se producen errores durante este proceso de configuración, detenga y póngase en contacto con el soporte técnico para obtener ayuda. No ignore los errores ni continúe en el proceso después de que se reciban los errores.  
  
## <a name="before-you-begin"></a>Antes de empezar  
Para configurar WSUS, debe:  
  
-   Tenga la información de inicio de sesión de la cuenta de administrador de dominio de Analytics Platform System Appliance.  
  
-   Tenga un inicio de sesión de System Analytics Platform con permisos para tener acceso a la **consola de administración** y ver la información de estado del dispositivo.  
  
-   Conozca la dirección IP del servidor WSUS que precede en la cadena si va a sincronizar las actualizaciones desde un servidor WSUS que precede en la cadena en lugar de sincronizar las actualizaciones directamente desde Microsoft Update. Asegúrese de que el servidor WSUS que precede en la cadena está configurado para permitir conexiones anónimas y admita SSL.  
  
-   Conozca la dirección IP del servidor proxy si el dispositivo va a usar un servidor proxy para acceder al servidor que precede en la cadena o a Microsoft Update.  
  
-   En la mayoría de los casos, WSUS necesita acceder a los servidores fuera del dispositivo. Para admitir este escenario de uso, el DNS del sistema de plataforma de análisis puede configurarse para admitir un reenviador de nombres externo que permita que los hosts de sistema de la plataforma de análisis y el Virtual Machines (VM) usen servidores DNS externos para resolver nombres fuera del dispositivo. Para obtener más información, consulte [uso de un reenviador DNS para resolver nombres DNS que no son de dispositivo &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="to-configure-windows-server-update-services-wsus"></a>Para configurar Windows Server Update Services (WSUS)  
  
1.  Inicie sesión en la **consola de administración**de. En la pestaña **Estado del dispositivo** , compruebe que las columnas **clúster** y **red** muestran el color verde (o **na**) de todos los nodos. Compruebe los indicadores de estado de todos los nodos en el **Estado del dispositivo**.  
  
    -   Es seguro continuar con los indicadores verde o NA.  
  
    -   Evaluar errores de advertencia no críticos (amarillos). En algunos casos, los mensajes de advertencia no bloquearán las actualizaciones. Si hay un error de volumen de disco no crítico que no está en el C:\ , puede continuar con el paso siguiente antes de resolver el error de volumen de disco.  
  
    -   La mayoría de los indicadores rojos se deben resolver antes de continuar. Si hay errores de disco, use la página de alertas de la **consola de administración** para comprobar que no haya más de un error de disco dentro de cada matriz de servidores o San. Si no hay más de un error de disco dentro de cada matriz de servidores o SAN, puede continuar con el paso siguiente antes de corregir los errores de disco. Asegúrese de ponerse en contacto con el soporte técnico de Microsoft para corregir los errores de disco lo antes posible.  
  
2.  Inicie sesión en la máquina virtual de VMM como administrador de dominio del dispositivo.  
  
3.  Inicie el Asistente para configuración.  
  
    #### <a name="to-launch-the-configuration-wizard"></a>Para iniciar el Asistente para configuración  
  
    1.  En el **Panel de administrador del servidor**, en el menú **herramientas** , haga clic en **Windows Server Update Services**.  
  
    2.  En el panel izquierdo de la ventana **servicios de actualización** , haga clic para expandir el servidor de nodo de administración de la máquina Virtual (**_appliance_domain_-VMM**) y, a continuación, haga clic en **Opciones**.  
  
    3.  En el panel **Opciones** , haga clic en Asistente para la **configuración del servidor WSUS** para iniciar el Asistente para configuración.  
  
        ![Menú del panel del Administrador del servidor](./media/configure-windows-server-update-services-wsus/WSUS_Wiz0.png "WSUS_Wiz0")  
  
    4.  Si es la primera vez que ejecuta el Asistente de WSUS, es posible que se le pida que configure un directorio para almacenar las actualizaciones. `C:\wsus` es una ubicación adecuada; sin embargo, puede proporcionar una ruta de acceso diferente.  
  
        ![WSUS - Ruta de acceso](./media/configure-windows-server-update-services-wsus/WSUS_Wiz1.png "WSUS_Wiz1")  
  
    5.  Revise la lista **antes de comenzar** de los elementos que se deben completar antes de completar el asistente.  
  
        ![WSUS - Antes de empezar](./media/configure-windows-server-update-services-wsus/WSUS_Wiz2.png "WSUS_Wiz2")  
  
    6.  En la página **unirse al programa de mejora de Microsoft Update** , seleccione **sí, deseo unirme al programa de mejora**de la Microsoft Update y, a continuación, haga clic en **siguiente**.  
  
        ![WSUS - Programa de mejora](./media/configure-windows-server-update-services-wsus/WSUS_Wiz3.png "WSUS_Wiz3")  
  
    Ahora debería ver la página **elegir servidor que precede** en la cadena. La captura de pantalla siguiente es el punto de partida del Asistente para configuración.  
  
    ![WSUS - Sincronizar servidor que precede en la cadena](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
4.  Elija el servidor que precede en la cadena.  
  
    En la página **elegir servidor que precede** en la cadena del Asistente para configuración de WSUS, seleccionará cómo se conectará WSUS en el nodo Administración de máquina virtual a un servidor que precede en la cadena para obtener actualizaciones de software. Las dos opciones son sincronizar el servidor que precede en la cadena con [Microsoft Update](https://go.microsoft.com/fwlink/?LinkId=133349) o sincronizar las actualizaciones con otro servidor de Windows Server Update Services.  
  
    #### <a name="to-update-by-using-microsoft-update"></a>Para actualizar mediante Microsoft Update  
  
    1.  Si decide sincronizar con Microsoft Update, no es necesario realizar ningún cambio en la página **elegir servidor que precede** en la cadena. Haga clic en **Siguiente**.  
  
        ![WSUS - Sincronizar servidor que precede en la cadena](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
    #### <a name="to-update-from-another-wsus-server"></a>Para actualizar desde otro servidor WSUS  
  
    1.  Si decide sincronizar con un origen que no sea Microsoft Update (un servidor que precede en la cadena), especifique el servidor (escriba la dirección IP) y el puerto en el que este servidor se comunicará con el servidor que precede en la cadena.  
  
        ![WSUS - Sincronizar servidor que precede en la cadena desde WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4b.png "WSUS_Wiz4b")  
  
    2.  Para usar Capa de sockets seguros (SSL), active la casilla **usar SSL al sincronizar la información de actualización** . En ese caso, los servidores usarán el puerto 443 para la sincronización.  
  
        ![WSUS - Sincronizar servidor que precede en la cadena desde SSL WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4c.png "WSUS_Wiz4c")  
  
    3.  Si este es un servidor de réplicas, active la casilla **Esto es una réplica del servidor que precede en la cadena**. Es posible seleccionar **usar SSL al sincronizar la información de actualización** y **se trata de una réplica del servidor que precede en la cadena**.  
  
        ![WSUS - Réplica del servidor que precede en la cadena](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4d.png "WSUS_Wiz4d")  
  
    4.  En este momento, ya ha terminado con la configuración del servidor que precede en la cadena. Haga clic en **siguiente**o seleccione **especificar servidor proxy** en el panel de navegación izquierdo.  
  
5.  Especifique el servidor proxy.  
  
    Si este servidor requiere un servidor proxy para tener acceso a Microsoft Update o a otro servidor que precede en la cadena, puede establecer la configuración del servidor proxy aquí; de lo contrario, haga clic en **siguiente**.  
  
    ![WSUS - Proxy](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5a.png "WSUS_Wiz5a")  
  
    #### <a name="to-configure-proxy-server-settings"></a>Para configurar el servidor proxy  
  
    1.  En la página **especificar servidor proxy** del Asistente para configuración, active la casilla **usar un servidor proxy al sincronizar** y, a continuación, escriba la dirección IP del servidor proxy (no nombre) y el número de puerto (puerto 80 de forma predeterminada) en los cuadros correspondientes.  
  
    2.  Si desea conectarse al servidor proxy con credenciales de usuario específicas, active la casilla **Usar credenciales de usuario para conectarse al servidor proxy** y, a continuación, escriba el nombre de usuario, el dominio y la contraseña del usuario en los cuadros correspondientes. Si desea habilitar la autenticación básica para el usuario que se conecta al servidor proxy, active la casilla **permitir autenticación básica (la contraseña se envía en texto no cifrado)** .  
  
        ![WSUS - Credenciales del proxy](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5b.png "WSUS_Wiz5b")  
  
    3.  En este momento, ya ha terminado con la configuración del servidor proxy. Haga clic en **Siguiente** para ir a la página siguiente, donde puede empezar a configurar el proceso de sincronización.  
  
6.  Iniciar la conexión.  
  
    ![WSUS - Inicio de conexión del proxy](./media/configure-windows-server-update-services-wsus/WSUS_Wiz6.png "WSUS_Wiz6")  
  
    Haga clic en **iniciar conexión**.  
  
    Una vez que la conexión se ha realizado correctamente, haga clic en **siguiente** para ir a la página siguiente, donde puede elegir idiomas.  
  
7.  Elija idiomas.  
  
    Seleccione **Descargar actualizaciones solo en estos idiomas**.  
  
    Seleccione **Inglés**y, a continuación, haga clic en **siguiente**.  
  
    ![Elegir idiomas](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseLanguages.png "SQL_Server_PDW_WSUSChooseLanguages")  
  
8.  Elija productos.  
  
    > [!NOTE]  
    > Si usa un servidor que precede en la cadena, es posible que no pueda elegir productos. Si esta opción no está disponible, omita este paso.

    > [!WARNING]  
    > Excluya las actualizaciones de SQL Server 2016.
  
    Anula la selección de todas las actualizaciones seleccionadas.  
  
    Seleccione **SQL Server 2012**, **SQL Server 2014**, **Windows Server 2012 R2**y **System Center 2012 R2-Virtual Machine Manager**y, a continuación, haga clic en **siguiente**.  
  
9. Elija clasificaciones.  
  
    > [!NOTE]  
    > Si usa un servidor que precede en la cadena, es posible que no pueda elegir las clasificaciones.  Si esta opción no está disponible, omita este paso.  
  
    Anular la selección de todas las actualizaciones seleccionadas previamente.  
  
    Seleccione **actualizaciones críticas** y actualizaciones de **seguridad** para las actualizaciones que se van a sincronizar para el dispositivo de sistema de plataforma de análisis y, a continuación, haga clic en **siguiente**.  
  
    ![Elegir clasificaciones](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseClassifications.png "SQL_Server_PDW_WSUSChooseClassifications")  
  
10. Configure la programación de sincronización.  
  
    Seleccione **sincronizar manualmente**y, a continuación, haga clic en **siguiente**.  
  
    ![Establecer programación de sincronización](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSyncSchedule.png "SQL_Server_PDW_WSUSSyncSchedule")  
  
11. Comenzar la sincronización inicial.  
  
    Seleccione **Iniciar sincronización inicial**y, a continuación, haga clic en **siguiente**.  
  
12. Finish. (Finalizar)  
  
    Haga clic en **Finalizar**  
  
## <a name="group-the-appliance-servers-in-wsus"></a><a name="bkmk_WSUSGroup"></a>Agrupar los servidores de la aplicación en WSUS  
Después de configurar WSUS para el sistema de plataforma de análisis, el siguiente paso es agrupar los servidores de la aplicación. Al agregar todos los servidores de dispositivo a un grupo, WSUS podrá aplicar actualizaciones de software a todos los servidores del dispositivo.  
  
> [!NOTE]  
> El sistema WSUS está diseñado para ejecutarse de forma asincrónica. La actividad de inicio no siempre produce una actualización inmediata. Por lo tanto, es posible que tenga que esperar un rato hasta que los equipos estén visibles en los cuadros de diálogo de WSUS. La ejecución del `setup.exe /action=ReportMicrosoftUpdateClientStatus /DomainAdminPassword="<password>"` comando que se describe al final del tema [descarga y aplicación de actualizaciones de Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md) puede ayudarle a actualizar los cuadros de diálogo.  
  
#### <a name="to-group-the-appliance-servers"></a>Para agrupar los servidores de la aplicación  
  
1.  Abra la consola de WSUS, haga clic con el botón secundario en **todos los equipos** y haga clic en **Agregar grupo de equipos**.  
  
    ![Agregue un grupo de equipos.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSAddComputerGroup.png "SQL_Server_PDW_WSUSAddComputerGroup")  
  
2.  Escriba el nombre "APS" para el grupo de equipos y, a continuación, haga clic en **Agregar**.  
  
    ![Escriba un nombre para el nuevo grupo de equipos.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSpecifyGroupName.png "SQL_Server_PDW_WSUSSpecifyGroupName")  
  
3.  Vuelva a hacer clic en **todos los equipos** , cambie el estado en el menú desplegable **Estado** a **cualquiera**y, a continuación, haga clic en **Actualizar**. Es posible que necesite expandir **todos los equipos** haciendo clic en el control de árbol de la izquierda para ver el nuevo grupo que acaba de agregar.  
  
    ![Cambie el estado a Cualquiera y haga clic en Actualizar.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusToAny.png "SQL_Server_PDW_WSUSChangeStatusToAny")  
  
4.  Seleccione todos los equipos que forman parte del dispositivo, haga clic con el botón secundario y, a continuación, haga clic en **cambiar pertenencia**.  
  
    ![Cambie la pertenencia para todos los equipos de PDW.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeMembership.png "SQL_Server_PDW_WSUSChangeMembership")  
  
5.  Seleccione el nuevo grupo de equipos que ha creado; para ello, haga clic en la casilla y, a continuación, haga clic en **Aceptar**.  
  
    ![Establecer la pertenencia del grupo de equipos](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSetComputerGroupMembership.png "SQL_Server_PDW_WSUSSetComputerGroupMembership")  
  
6.  Seleccione el nuevo grupo de equipos, cambie su **Estado** a **cualquiera**y, a continuación, haga clic en **Actualizar**. Ahora todos los equipos deben estar asignados a este grupo y aparecer en el panel derecho. Por lo general, es seguro continuar cuando los nodos muestran advertencias, como que **este nodo todavía no ha notificado el estado**.  
  
    ![Cambie el estado a cualquiera y haga clic en actualizar.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusAnyRefresh.png "SQL_Server_PDW_WSUSChangeStatusAnyRefresh")  
