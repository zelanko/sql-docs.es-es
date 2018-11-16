---
title: Configurar WSUS - Analytics Platform System | Microsoft Docs
description: Estas instrucciones le guiarán a través de los pasos para usar al Asistente para que configuración de Windows Server Update Services (WSUS) para configurar WSUS para Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0b79db4806f22c7d25af4f292fedddb46b40d1e7
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51696944"
---
# <a name="configure-windows-server-update-services-wsus-in-analytics-platform-system"></a>Configurar Windows Server Update Services (WSUS) de Analytics Platform System
Estas instrucciones le guiarán a través de los pasos para usar al Asistente para que configuración de Windows Server Update Services (WSUS) para configurar WSUS para Analytics Platform System. Deberá configurar WSUS antes de aplicar las actualizaciones de software para el dispositivo. WSUS se ha instalado en la máquina virtual VMM del dispositivo.  
  
Para obtener más información sobre la configuración de WSUS, consulte el [Guía de instalación paso a paso de WSUS](https://go.microsoft.com/fwlink/?LinkId=202417) en el sitio Web WSUS. Después de configurar WSUS, consulte [descarga y se aplican las actualizaciones de Microsoft &#40;Analytics Platform System&#41; ](download-and-apply-microsoft-updates.md) para iniciar una actualización.  
  
> [!WARNING]  
> Si encuentra algún error durante este proceso de configuración, detenga y póngase en contacto con soporte técnico para obtener ayuda. No omita los errores o continuar en el proceso después de que se reciben errores.  
  
## <a name="before-you-begin"></a>Antes de comenzar  
Para configurar WSUS, deberá:  
  
-   Tiene la información de inicio de sesión de cuenta de Analytics Platform System appliance dominio administrador.  
  
-   Tener un inicio de sesión de Analytics Platform System con permisos para tener acceso a la **Admin Console** y ver información de estado del dispositivo.  
  
-   Si va a sincronizar las actualizaciones desde un servidor WSUS ascendente en lugar de sincronizar las actualizaciones directamente desde Microsoft Update, sabe la dirección IP del servidor WSUS ascendente. Asegúrese de que el servidor WSUS ascendente se establece para permitir conexiones anónimas y es compatible con SSL.  
  
-   Conocer la dirección IP del servidor proxy si su dispositivo va a utilizar un servidor proxy para tener acceso al servidor que precede o Microsoft Update.  
  
-   En la mayoría de los casos, WSUS necesita acceso a los servidores están fuera de la aplicación. Para admitir este escenario de uso, el sistema de plataforma de análisis de DNS puede configurarse para admitir un reenviador de nombre externo que permitirá a los hosts de Analytics Platform System y la máquinas virtuales (VM) usar servidores DNS externos para resolver nombres fuera de la dispositivo. Para obtener más información, consulte [usar un reenviador DNS para resolver los nombres DNS que no son de dispositivo &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="to-configure-windows-server-update-services-wsus"></a>Para configurar Windows Server Update Services (WSUS)  
  
1.  Inicie sesión en el **consola de administración**. En el **estado de dispositivo** , compruebe que la **clúster** y **red** columnas muestran verde (o **NA**) para todos los nodos. Compruebe los indicadores de estado para todos los nodos en el **estado de dispositivo**.  
  
    -   Es seguro continuar con el color verde o indicadores NA.  
  
    -   Evaluar errores no críticos de advertencia (amarillo). En algunos casos los mensajes de advertencia no bloqueará las actualizaciones. Si se produce un error de volumen de disco no críticos que no está en la unidad C:\, puede continuar con el paso siguiente antes de resolver el error de volumen de disco.  
  
    -   La mayoría de los indicadores rojo se deben resolver antes de continuar. Si hay errores de disco, use la **consola de administración de alertas** página para comprobar que hay un error de no más de un disco en cada servidor o una matriz de SAN. Si se produce un error de no más de un disco en cada servidor o una matriz de SAN, puede continuar con el paso siguiente antes de corregir los errores de disco. Asegúrese de ponerse en contacto con soporte técnico de Microsoft para corregir los errores de disco tan pronto como sea posible.  
  
2.  Inicie sesión en la máquina virtual VMM como un administrador de dominio del equipo.  
  
3.  Inicie al Asistente para configuración.  
  
    #### <a name="to-launch-the-configuration-wizard"></a>Para iniciar al Asistente para configuración  
  
    1.  En el **panel Administrador del servidor**, en el **herramientas** menú, haga clic en **Windows Server Update Services**.  
  
    2.  En el panel izquierdo de la **Update Services** ventana, haga clic para expandir el servidor de administración de máquinas virtuales de nodos (***appliance_domain *-VMM**) y, a continuación, haga clic en **opciones**.  
  
    3.  En el **opciones** panel, haga clic en **Asistente para configuración de servidor de WSUS** para iniciar el Asistente para configuración.  
  
        ![Menú del panel del administrador del servidor](./media/configure-windows-server-update-services-wsus/WSUS_Wiz0.png "WSUS_Wiz0")  
  
    4.  Si se trata de la primera vez que ejecuta el Asistente para WSUS, se le pedirá que configure un directorio para almacenar las actualizaciones. `C:\wsus` es una ubicación adecuada; Sin embargo puede proporcionar una ruta de acceso diferente.  
  
        ![Ruta de acceso WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz1.png "WSUS_Wiz1")  
  
    5.  Revise el **antes de comenzar** lista de elementos que se complete antes de completar el asistente.  
  
        ![WSUS antes de comenzar](./media/configure-windows-server-update-services-wsus/WSUS_Wiz2.png "WSUS_Wiz2")  
  
    6.  En el **unirse al programa de mejora de Microsoft Update** página, seleccione **Sí, me gustaría unirse al programa de mejora de Microsoft Update**y, a continuación, haga clic en **siguiente**.  
  
        ![Programa para la mejora WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz3.png "WSUS_Wiz3")  
  
    Ahora debería ver el **Elegir servidor que precede** página. Captura de pantalla siguiente es el punto inicial del Asistente para configuración.  
  
    ![WSUS-Sincronizar servidor que precede en](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
4.  Elija el servidor que precede.  
  
    En el **Elegir servidor que precede** página del Asistente para configuración de WSUS, seleccionará cómo WSUS en el nodo de administración de máquinas virtuales se conectarán a un servidor de nivel superior para obtener actualizaciones de software. Son las dos opciones sincronizar con el servidor que precede [Microsoft Update](https://go.microsoft.com/fwlink/?LinkId=133349) o sincronizar las actualizaciones con otro servidor de Windows Server Update Services.  
  
    #### <a name="to-update-by-using-microsoft-update"></a>Actualizar con Microsoft Update  
  
    1.  Si elige sincronizar con Microsoft Update, no es necesario realizar ningún cambio a la **Elegir servidor que precede** página. Haga clic en **Siguiente**.  
  
        ![WSUS-Sincronizar servidor que precede en](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
    #### <a name="to-update-from-another-wsus-server"></a>Para actualizar desde otro servidor WSUS  
  
    1.  Si elige sincronizar con un origen que no sea de Microsoft Update (un servidor que precede), especifique el servidor (escriba la dirección IP) y el puerto en el que este servidor se comunicará con el servidor que precede.  
  
        ![WSUS-Sincronizar servidor que precede desde WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4b.png "WSUS_Wiz4b")  
  
    2.  Para usar capa de Sockets seguros (SSL), seleccione el **usar SSL al sincronizar información sobre la actualización** casilla de verificación. En ese caso, los servidores utilizarán el puerto 443 para la sincronización.  
  
        ![WSUS-Sincronizar servidor que precede desde SSL WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4c.png "WSUS_Wiz4c")  
  
    3.  Si se trata de un servidor de réplica, seleccione el **se trata de una réplica del servidor ascendente** casilla de verificación. Es posible seleccionar ambos **usar SSL al sincronizar la información de actualización** y **se trata de una réplica del servidor que precede en la cadena**.  
  
        ![Réplica del servidor que precede en WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4d.png "WSUS_Wiz4d")  
  
    4.  En este momento, ya ha terminado con la configuración del servidor que precede. Haga clic en **siguiente**, o bien seleccione **especificar servidor de proxy** en el panel de navegación izquierdo.  
  
5.  Especifique el servidor proxy.  
  
    Si este servidor requiere un servidor proxy para tener acceso a Microsoft Update o un servidor que precede en diferentes, puede configurar aquí; la configuración del servidor proxy en caso contrario, haga clic en **siguiente**.  
  
    ![WSUS-Proxy](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5a.png "WSUS_Wiz5a")  
  
    #### <a name="to-configure-proxy-server-settings"></a>Para configurar el servidor proxy  
  
    1.  En el **especificar servidor Proxy** página del Asistente de configuración, seleccione el **utilizar un servidor proxy al sincronizar** casilla de verificación y, a continuación, escriba la dirección IP del servidor proxy (no por el nombre) y el número de puerto (puerto 80, valor predeterminado) en los cuadros correspondientes.  
  
    2.  Si desea conectarse al servidor proxy con credenciales de usuario específicas, seleccione el **usar las credenciales de usuario para conectarse al servidor proxy** casilla de verificación y, a continuación, escriba el nombre de usuario, dominio y contraseña del usuario en las correspondientes cuadros. Si desea habilitar la autenticación básica para el usuario se conecta al servidor proxy, seleccione el **permitir autenticación básica (la contraseña se envía en texto no cifrado)** casilla de verificación.  
  
        ![Las credenciales de Proxy WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5b.png "WSUS_Wiz5b")  
  
    3.  En este momento, ya ha terminado con la configuración del servidor proxy. Haga clic en **siguiente** para ir a la página siguiente, donde puede empezar a configurar el proceso de sincronización.  
  
6.  Comenzar a conectar.  
  
    ![WSUS-Proxy comenzar a conectar](./media/configure-windows-server-update-services-wsus/WSUS_Wiz6.png "WSUS_Wiz6")  
  
    Haga clic en **comenzar a conectar**.  
  
    Después de la conexión se ha realizado correctamente, haga clic en **siguiente** para ir a la página siguiente, donde puede elegir los idiomas.  
  
7.  Elegir idiomas.  
  
    Seleccione **descargar actualizaciones solamente en estos idiomas**.  
  
    Seleccione **inglés**y, a continuación, haga clic en **siguiente**.  
  
    ![Elegir idiomas](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseLanguages.png "SQL_Server_PDW_WSUSChooseLanguages")  
  
8.  Elija los productos.  
  
    > [!NOTE]  
    > Si usa un servidor ascendente, es posible que no podrá elegir productos. Si esta opción no está disponible, omita este paso.  
  
    Anule la selección de todas las actualizaciones seleccionadas.  
  
    Seleccione **Windows Server 2012 R2**, y **System Center 2012 R2 - Virtual Machine Manager**y, a continuación, haga clic en **siguiente**.  
  
9. Elegir clasificaciones.  
  
    > [!NOTE]  
    > Si usa un servidor ascendente, es posible que no podrá elegir clasificaciones.  Si esta opción no está disponible, omita este paso.  
  
    Anule la selección de todas las actualizaciones seleccionadas previamente.  
  
    Seleccione **actualizaciones críticas** y **las actualizaciones de seguridad** para las actualizaciones que se sincronizarán para el dispositivo de Analytics Platform System y, a continuación, haga clic en **siguiente**.  
  
    ![Elegir clasificaciones](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseClassifications.png "SQL_Server_PDW_WSUSChooseClassifications")  
  
10. Configure la programación de sincronización.  
  
    Seleccione **sincronizar manualmente**y, a continuación, haga clic en **siguiente**.  
  
    ![Establecer programación de sincronización](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSyncSchedule.png "SQL_Server_PDW_WSUSSyncSchedule")  
  
11. Iniciar la sincronización inicial.  
  
    Seleccione **iniciar sincronización inicial**, a continuación, haga clic en **siguiente**.  
  
12. Finalizar.  
  
    Haga clic en **Finalizar**.  
  
## <a name="bkmk_WSUSGroup"></a>Agrupar los servidores de dispositivo de WSUS  
Después de configurar WSUS para Analytics Platform System, el siguiente paso es agrupar los servidores de aplicación. Mediante la adición de todos los servidores de dispositivo a un grupo, WSUS se podrán realizar las actualizaciones de software se aplican a todos los servidores en el dispositivo.  
  
> [!NOTE]  
> El sistema WSUS está diseñado para ejecutarse de forma asincrónica. Iniciando la actividad no siempre produce una actualización inmediata. Por lo tanto, es posible que necesite, espere hasta que los equipos estarán visibles en los cuadros de diálogo WSUS. Ejecuta el `setup.exe /action=ReportMicrosoftUpdateClientStatus /DomainAdminPassword="<password>"` comando que se describe al final del tema [descarga y se aplican las actualizaciones de Microsoft &#40;Analytics Platform System&#41; ](download-and-apply-microsoft-updates.md) puede ayudar a los cuadros de diálogo de actualización.  
  
#### <a name="to-group-the-appliance-servers"></a>Para agrupar los servidores de dispositivo  
  
1.  Abra la consola WSUS, haga clic en **todos los equipos** y, a continuación, haga clic en **Agregar grupo de equipos**.  
  
    ![Agregar un grupo de equipos. ](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSAddComputerGroup.png "SQL_Server_PDW_WSUSAddComputerGroup")  
  
2.  Escriba el nombre "AP" para el grupo de equipos y, a continuación, haga clic en **agregar**.  
  
    ![Escriba el nombre para el nuevo grupo de equipos. ](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSpecifyGroupName.png "SQL_Server_PDW_WSUSSpecifyGroupName")  
  
3.  Haga clic en **todos los equipos** nuevo, cambie el estado en el **estado** menú desplegable para **cualquier**y, a continuación, haga clic en **actualizar**. Es posible que deba expandir **todos los equipos** haciendo clic en él en el control de árbol de la izquierda para ver el nuevo grupo que acaba de agregar.  
  
    ![Cambie el estado a cualquiera y haga clic en actualizar. ](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusToAny.png "SQL_Server_PDW_WSUSChangeStatusToAny")  
  
4.  Seleccione todos los equipos que forman parte de la aplicación, contextual y, a continuación, haga clic en **cambiar pertenencia**.  
  
    ![Cambiar la pertenencia de todos los equipos PDW. ](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeMembership.png "SQL_Server_PDW_WSUSChangeMembership")  
  
5.  Seleccione el nuevo grupo de equipos que ha creado haciendo clic en la casilla de verificación y, a continuación, haga clic en **Aceptar**.  
  
    ![Pertenencia al grupo de equipos del conjunto](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSetComputerGroupMembership.png "SQL_Server_PDW_WSUSSetComputerGroupMembership")  
  
6.  Seleccione el nuevo grupo de equipos, cambiar su **estado** a **cualquier**y, a continuación, haga clic en **actualizar**. Todos los equipos ahora deben ser asignados a este grupo y aparece en el panel derecho. Por lo general es seguro continuar cuando los nodos muestran las advertencias como **este nodo no ha notificado estado aún**.  
  
    ![Cambie el estado a cualquiera y haga clic en actualizar. ](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusAnyRefresh.png "SQL_Server_PDW_WSUSChangeStatusAnyRefresh")  
  
