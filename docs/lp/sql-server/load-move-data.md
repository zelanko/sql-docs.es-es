---
layout: HubPage
hide_bc: true
title: SQL Server - Cargar y mover datos
description: Explore las características que le ayudan a cargar, mover y migrar las bases de datos y los datos con SQL Server.
ms.topic: hub-page
featureFlags:
- clicktale
ms.openlocfilehash: 50ad47c11ccba509399104f019aaa07080299fd8
ms.sourcegitcommit: 97463ffe99915f3bbdf298e6e6b8d170e738ea7a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/17/2018
ms.locfileid: "49390857"
---
<div id="main" class="v2">
    <div class="container">
        <ul class="cardsY panelContent featuredContent">
            <li>
                <a href="https://www.microsoft.com/sql-server/sql-server-downloads">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/download-sql-server.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">Descargar SQL Server</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>
            <li>
                <a href="https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/get-azure-sql-vm.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">Obtener una máquina virtual con SQL Server</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>
            <li>
                <a href="/sql/ssms/download-sql-server-management-studio-ssms">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/download-ssms.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">Descargar SQL Server Management Studio</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>              
        </ul>
    </div>
    <div class="container">
        <h1>SQL Server: migración, carga y movimiento de datos</h1>
        <ul class="pivots tabLess">
            <li class="pivotItem" style="display: list-item;" data-id="#products">
                <a href="#products" data-linktype="self-bookmark"></a>
                <ul id="products">
                    <li class="panelItem" data-index="0">
                        <a class="singlePanelNavItem selected" href="#products1" data-linktype="self-bookmark"></a>
                        <ul class="cardsD panelContent singlePanelContent" id="products1" style="margin-top: 0px; display: flex;">
                            <li class="fullSpan">
                                <div class="container intro">
                                <h2>Migrar bases de datos a SQL</h2>
                            </li>
                                                         <li>
                                <a href="/azure/dms/dms-overview/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/install-sql-and-services/adm-service.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Azure Database Migration Service</h3>
                                                    <p>Permite migraciones sin problemas desde varios orígenes de base de datos a plataformas de datos de Azure con el tiempo de inactividad mínimo.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/dma/dma-overview/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/install-sql-and-services/dma-assist.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Database Migration Assistant (DMA)</h3>
                                                    <p>Detecta problemas de compatibilidad, recomienda mejoras para su entorno de destino y mueve su base de datos y sus datos.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/ssma/sql-server-migration-assistant/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/install-sql-and-services/ssma-assist.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>SQL Server Migration Assistant (SSMA)</h3>
                                                    <p>Automatiza la migración de bases de datos a SQL Server desde Microsoft Access, DB2, MySQL, Oracle y SAP ASE.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/dea/database-experimentation-assistant-overview">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/load-move-data/database-experimentation-assistant.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Asistente para experimentación con bases de datos (DEA)</h3>
                                                    <p>Ayuda a evaluar una versión de destino de SQL Server para una carga de trabajo existente.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li class="fullSpan">
                                <div class="container intro">
                                <h2>Cargar y mover los datos</h2>
                            </li>
                            <li>
                                <a href="/sql/tools/bcp-utility/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/load-move-data/bcp.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>BCP</h3>
                                                    <p>Copie datos de forma masiva entre un archivo de datos, en un formato que especifique y su base de datos SQL.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> 
                            <li>
                                <a href="/sql/relational-databases/import-export/import-flat-file-wizard">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/load-move-data/flat-file-import-wizard.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Asistente para la importación de archivos planos</h3>
                                                    <p>Use el asistente como una forma sencilla de copiar datos de un archivo plano (.csv, .txt) en su base de datos SQL. </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/load-move-data/import-export-wizard.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Asistente para importación y exportación</h3>
                                                    <p>Use el asistente como una forma sencilla de copiar datos de una amplia variedad de orígenes en su base de datos SQL. </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/integration-services/sql-server-integration-services">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/load-move-data/ssis.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>SQL Server Integration Services (SSIS)</h3>
                                                    <p>Extraiga y transforme datos de diversos orígenes como archivos planos y orígenes de datos relacionales y, después, cargar los datos en su base de datos SQL. </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/replication/sql-server-replication/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/load-move-data/replication.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>REPLICATION</h3>
                                                    <p> Un conjunto de tecnologías destinadas a la copia y distribución de datos y objetos de base de datos de una base de datos a otra, para luego sincronizar ambas bases de datos con el fin de mantener su coherencia.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                        </ul>
                    </li>
                </ul>
            </li>
        </ul>
    </div>
</div>
<div class="container centered pageFooter">
        <h2>Manténgase en contacto con nosotros</h2>
        <ul class="links">
           <li>
                <a href="http://aka.ms/editsqldocs" data-linktype="external"> Contribuir </a>
            </li>
           <li>
                <a href="https://docs.microsoft.com/sql/sql-server/sql-server-get-help" data-linktype="external"> Obtener ayuda </a>
            </li>
           <li>
                <a href="http://aka.ms/sqldocsfeedback" data-linktype="external"> Comentarios </a>
            </li>
           <li>
                <a href="http://aka.ms/sqldocsurvey" data-linktype="external"> Encuesta </a>
            </li>
           <li>
                <a href="https://cloudblogs.microsoft.com/sqlserver/" data-linktype="external"> Blog </a>
            </li>
            <li>
                <a href="https://twitter.com/sqldocs" data-linktype="external"> Twitter </a>
            </li>
            <li>
                <a href="https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqldatabaseengine&filter=alltypes&sort=lastpostdesc" data-linktype="external"> Foro de MSDN </a>
            </li>
            <li>
                <a href="https://feedback.azure.com/forums/908035-sql-server" data-linktype="external"> UserVoice </a>
            </li>
        </ul>
    </div>

