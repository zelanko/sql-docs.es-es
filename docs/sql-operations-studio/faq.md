---
title: SQL Operations Studio (preview) preguntas más frecuentes | Documentos de Microsoft
description: Preguntas más frecuentes (P+F) para las SQL Operations Studio (preview).
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ede16ad2aaafd14671cc9e58a4643a07ae85668a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="includename-sosincludesname-sosmd-faq"></a>[!INCLUDE[name-sos](../includes/name-sos.md)]PREGUNTAS MÁS FRECUENTES

## <a name="what-is-includename-sosincludesname-sos-shortmd"></a>¿Qué es [!INCLUDE[name-sos](../includes/name-sos-short.md)]?

[!INCLUDE[name-sos](../includes/name-sos-short.md)]es una herramienta de desarrollo y las operaciones de base de datos ligera gratuita que se ejecuta en el escritorio y está disponible para Windows, Mac OS y Linux. [!INCLUDE[name-sos](../includes/name-sos-short.md)]tiene compatibilidad integrada para la base de datos de SQL Azure, almacenamiento de datos de SQL Azure y SQL Server que se ejecuta de forma local o en cualquier nube. [!INCLUDE[name-sos](../includes/name-sos-short.md)]ofrece una experiencia coherente a través de las bases de datos de su elección en sus sistemas operativos favoritos.

## <a name="where-can-i-get-includename-sosincludesname-sos-shortmd"></a>¿Dónde puedo obtener [!INCLUDE[name-sos](../includes/name-sos-short.md)]?

Descargar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Windows, Mac OS y Linux desde [http://aka.ms/sqlopsstudio](download.md)

## <a name="how-much-does-includename-sosincludesname-sos-shortmd-cost"></a>¿Cuánto [!INCLUDE[name-sos](../includes/name-sos-short.md)] costo?

[!INCLUDE[name-sos](../includes/name-sos-short.md)]está disponible para el uso comercial o privada.

## <a name="who-should-use-includename-sosincludesname-sos-shortmd"></a>¿Quién debe usar [!INCLUDE[name-sos](../includes/name-sos-short.md)]?

Cualquier persona puede usar [!INCLUDE[name-sos](../includes/name-sos-short.md)]. Sin embargo, está diseñado para simplificar las tareas realizadas por los desarrolladores de base de datos, los administradores de base de datos, los administradores del sistema y fabricantes independientes de software.


## <a name="what-can-i-do-with-includename-sosincludesname-sos-shortmd"></a>¿Qué puedo hacer con [!INCLUDE[name-sos](../includes/name-sos-short.md)]? 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]se basa en el código de Visual Studio y ofrece una ligera, experiencia de flujo de trabajo de código modernas de foco de teclado cuando se trabaja con SQL. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]hace que las experiencias de núcleo que se basan en cada día simple y fácil con características integradas como varias ventanas de ficha, un editor enriquecido de SQL, IntelliSense, finalización de la palabra clave, fragmentos de código & navegación por el código y la integración de control de código fuente (Git y TFS). Puede ejecutar consultas a petición, ver & Guardar los resultados como texto, JSON o Excel, editar datos, organizar & Administrar las conexiones de base de datos favoritos y examinar objetos de base de datos en un objeto conocido experiencia de exploración.

Utilice las herramientas de línea de comandos (por ejemplo, Bash, PowerShell, sqlcmd, bcp, psql y ssh) en la ventana de Terminal integrado directamente la [!INCLUDE[name-sos](../includes/name-sos-short.md)] interfaz de usuario. Generar y ejecutar CREATE fácilmente y secuencias de comandos de INSERCIÓN para los objetos de base de datos crear copias de la base de datos para el desarrollo o con fines de prueba. Aumentar la productividad con código inteligente fragmentos de código y enriquecidas gráficas experiencias que crean nuevas bases de datos y objetos de base de datos (como tablas, vistas, procedimientos almacenados, los usuarios, los inicios de sesión, roles, etc.) o actualizar los objetos de base de datos existentes. Use paneles muy personalizables completos para supervisar y solucionar rápidamente los cuellos de botella de rendimiento en las bases de datos local, en Azure o en cualquier nube.

[!INCLUDE[name-sos](../includes/name-sos-short.md)]ofrece una experiencia coherente para copia de seguridad y restaurar las bases de datos. Con soporte planificado para SQL Server grupos de disponibilidad AlwaysOn, fácilmente puede configurar, supervisar y solucionar problemas de grupos de disponibilidad para bases de datos de SQL Server críticas y rápidamente conmutación por error a una base de datos secundaria durante un desastre.
[!INCLUDE[name-sos](../includes/name-sos-short.md)]se ha diseñado para ser más productivo en el ciclo de vida de DevOps de las bases de datos de elección en los sistemas operativos de su elección. Como resultado, siempre tiene el control, y puede reducir los riesgos, problemas con mayor rapidez y entregar continuamente valor que supera las expectativas de los clientes.


## <a name="is-includename-sosincludesname-sos-shortmd-open-source"></a>¿Es [!INCLUDE[name-sos](../includes/name-sos-short.md)] código abierto? 

El código fuente de [!INCLUDE[name-sos](../includes/name-sos-short.md)] y sus proveedores de datos está disponible en GitHub. El código fuente para el front-end de [!INCLUDE[name-sos](../includes/name-sos-short.md)] (que se basa en código de Visual Studio) está disponible en un código fuente términos de licencia que proporciona derechos para modificar y utilizar el software, pero no para redistribuir el control u hospedarlo en un servicio de nube. El código fuente para los proveedores de datos está disponible bajo la licencia MIT en [https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice).

## <a name="do-you-plan-to-open-source-ssms"></a>¿Tiene pensado Abrir origen SSMS?

No. Sin embargo, la generación siguiente herramientas CLI y GUI de multi-OS son código abierto. Por ejemplo, la extensión de mssql para el código de VS, mssql generador de scripts y msql CLI son todos los código abierto en GitHub. El código fuente de [!INCLUDE[name-sos](../includes/name-sos-short.md)] está disponible en GitHub.


## <a name="now-that-there-is-includename-sosincludesname-sos-shortmd-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>Ahora que hay [!INCLUDE[name-sos](../includes/name-sos-short.md)], ¿Microsoft planea degradar SSMS y SSDT?

No. Las inversiones en herramientas de Windows de estrella (SSMS, SSDT, PowerShell) seguirán además de la siguiente generación de multi-OS y herramientas CLI y GUI de multi-DB.
El objetivo es ofrecer a los clientes la posibilidad de utilizar las herramientas que deseen en las plataformas de su elección para sus escenarios.


## <a name="includename-sosincludesname-sos-shortmd-is-missing-a-feature-that-is-in-ssmsssdt-will-you-add-it"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)]Falta una característica que se encuentra en SSMS/SSDT. ¿Se agregará?
Depende de la necesidad de escenario de & cliente o business. Para ayudar a priorizar, una sugerencia de archivos en [GitHub](https://github.com/microsoft/sqlopsstudio/issues).


## <a name="i-understand-includename-sosincludesname-sos-shortmd-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>Entiendo [!INCLUDE[name-sos](../includes/name-sos-short.md)] y la extensión de mssql para el código de VS se basan en una nueva *herramientas servicio* que usa las API de SMO en segundo plano. ¿Está disponible en Linux y macOS SMO?

Las API de SMO aún no están disponibles en Linux o Mac OS en una forma compatible. Se transfieren a través de un subconjunto de las API de SMO para .NET Core que necesitábamos para [!INCLUDE[name-sos](../includes/name-sos-short.md)], y tenemos previsto expandir como parte del plan.
El servicio de herramientas de SQL está en GitHub: [https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice).


## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>¿Tiene pensado trasladar la DACFx APIs o sqlpackage.exe o SSDT para Linux y macOS?

Está en el plan a largo plazo. Para ayudar a priorizar, una sugerencia de archivos en [GitHub](https://github.com/microsoft/sqlopsstudio/issues).


## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>¿Estará disponible en Linux y macOS cmdlets de PowerShell de SQL?

PowerShell de SQL está disponible actualmente en la Galería de PowerShell y se puede usar en Windows para trabajar con SQL Server en ejecución en cualquier lugar, incluido SQL en Linux. Oferta de SQL PowerShell cmdlets de Linux & macOS es en el plan. Para ayudar a priorizar, una sugerencia de archivos en [GitHub](https://github.com/microsoft/sqlopsstudio/issues).

