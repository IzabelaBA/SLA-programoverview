<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Service Tasks</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Salesforce Sans', -apple-system, BlinkMacSystemFont, sans-serif;
            background: #f3f3f3;
            color: #181818;
            padding: 2rem;
        }

        .program-header {
            max-width: 1600px;
            margin: 0 auto 1.5rem auto;
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            padding: 1.5rem 2rem;
        }

        .program-title {
            font-size: 1.5rem;
            font-weight: 700;
            color: #181818;
            margin: 0;
        }

        .main-container {
            max-width: 1600px;
            margin: 0 auto;
            display: flex;
            gap: 1.5rem;
        }

        .packages-sidebar {
            flex: 0 0 280px;
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            overflow: hidden;
            height: fit-content;
        }

        .packages-header {
            background: #f8f9fa;
            padding: 1rem;
            border-bottom: 1px solid #e5e5e5;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .packages-info {
            padding: 0.75rem 1rem;
            border-bottom: 1px solid #e5e5e5;
        }

        .packages-search {
            padding: 0.75rem 1rem;
            border-bottom: 1px solid #e5e5e5;
        }

        .packages-list {
            padding: 0.5rem 0;
        }

        .package-item {
            display: flex;
            align-items: center;
            padding: 0.75rem 1rem;
            cursor: pointer;
            transition: background-color 0.2s ease;
        }

        .package-item:hover {
            background: #f8f9fa;
        }

        .package-item.active {
            background: #e8f4fd;
            border-left: 3px solid #0176D3;
        }

        .package-name {
            font-weight: 600;
            color: #181818;
            font-size: 0.875rem;
            margin-bottom: 0.25rem;
        }

        .package-type {
            font-size: 0.75rem;
            color: #706E6B;
        }

        .left-section {
            flex: 1;
        }

        .right-section {
            flex: 0 0 350px;
        }

        .container {
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        .header {
            background: #f8f9fa;
            padding: 1.5rem;
            border-bottom: 1px solid #e5e5e5;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .header h1 {
            font-size: 1.25rem;
            font-weight: 600;
            color: #181818;
        }

        .table-container {
            overflow-x: auto;
        }

        .service-table {
            width: 100%;
            border-collapse: collapse;
            background: white;
        }

        .service-table th {
            background: #f8f9fa;
            padding: 0.5rem;
            text-align: left;
            font-weight: 600;
            font-size: 0.875rem;
            color: #3E3E3C;
            border-bottom: 2px solid #e5e5e5;
            white-space: nowrap;
        }

        .service-table td {
            padding: 0.5rem;
            border-bottom: 1px solid #e5e5e5;
            vertical-align: top;
        }

        .service-table tbody tr:hover {
            background: #f8f9fa;
        }

        .task-row {
            transition: background-color 0.2s ease;
        }

        .service-name {
            font-weight: 600;
            color: #0176D3;
            font-size: 0.875rem;
            cursor: pointer;
            text-decoration: underline;
        }

        .service-name:hover {
            color: #014486;
        }

        .col-service { width: 30%; }
        .col-date { width: 20%; }
        .col-assigned { width: 30%; }
        .col-status { width: 20%; }

        /* Tabs Styling */
        .tabs-container {
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        .tabs-nav {
            display: flex;
            background: #f8f9fa;
            border-bottom: 1px solid #e5e5e5;
        }

        .tab-button {
            flex: 1;
            padding: 1rem;
            background: none;
            border: none;
            font-size: 0.875rem;
            font-weight: 600;
            color: #706E6B;
            cursor: pointer;
            border-bottom: 2px solid transparent;
            transition: all 0.2s ease;
        }

        .tab-button:hover {
            color: #0176D3;
            background: #f0f8ff;
        }

        .tab-button.active {
            color: #0176D3;
            border-bottom-color: #0176D3;
            background: white;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        .info-section {
            margin-bottom: 1.5rem;
        }

        .info-label {
            font-size: 0.75rem;
            color: #706E6B;
            text-transform: uppercase;
            letter-spacing: 0.025em;
            margin-bottom: 0.25rem;
        }

        .info-value {
            font-weight: 600;
            color: #181818;
            font-size: 0.875rem;
        }

        .info-value.link {
            color: #0176D3;
            text-decoration: underline;
            cursor: pointer;
        }

        .info-value.status {
            color: #0176D3;
        }

        .contact-card {
            background: #f8f9fa;
            border: 1px solid #e5e5e5;
            border-radius: 6px;
            padding: 1rem;
            margin-bottom: 1rem;
        }

        .contact-name {
            font-weight: 600;
            color: #181818;
            margin-bottom: 0.5rem;
        }

        .contact-detail {
            margin-bottom: 0.25rem;
            font-size: 0.75rem;
        }

        .contact-detail-label {
            color: #706E6B;
            display: inline-block;
            width: 100px;
        }

        .contact-detail-value {
            color: #181818;
        }

        .contact-detail-value.email {
            color: #0176D3;
            text-decoration: underline;
        }

        .contact-detail-value.survey-yes {
            color: #04844B;
            font-weight: 600;
        }

        /* Button Styles */
        .btn {
            padding: 0.75rem 1.5rem;
            border-radius: 6px;
            font-weight: 600;
            font-size: 0.875rem;
            cursor: pointer;
            border: none;
            transition: all 0.2s ease;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
        }

        .btn-primary {
            background: #0176D3;
            color: white;
        }

        .btn-primary:hover {
            background: #014486;
        }

        .btn-secondary {
            background: white;
            color: #0176D3;
            border: 1px solid #0176D3;
        }

        .btn-secondary:hover {
            background: #f8f9fa;
        }

        /* Modal Styles */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
        }

        .modal {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            border-radius: 8px;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.2);
            width: 600px;
            max-width: 90vw;
            z-index: 1001;
        }

        .modal-header {
            padding: 1.5rem;
            border-bottom: 1px solid #e5e5e5;
            background: #f8f9fa;
            border-radius: 8px 8px 0 0;
            position: relative;
        }

        .modal-title {
            font-size: 1.25rem;
            font-weight: 600;
            color: #181818;
            margin: 0;
        }

        .modal-body {
            padding: 1.5rem;
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-label {
            display: block;
            font-weight: 600;
            color: #3E3E3C;
            font-size: 0.875rem;
            margin-bottom: 0.5rem;
        }

        .form-select {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #D8D8D8;
            border-radius: 4px;
            font-size: 0.875rem;
            background: white;
        }

        .form-select:focus {
            outline: none;
            border-color: #0176D3;
            box-shadow: 0 0 0 2px rgba(1, 118, 211, 0.1);
        }

        .modal-actions {
            padding: 1rem 1.5rem;
            border-top: 1px solid #e5e5e5;
            background: #f8f9fa;
            display: flex;
            justify-content: flex-end;
            gap: 0.75rem;
            border-radius: 0 0 8px 8px;
        }

        .close-btn {
            position: absolute;
            top: 1rem;
            right: 1rem;
            background: none;
            border: none;
            font-size: 1.5rem;
            color: #706E6B;
            cursor: pointer;
            width: 2rem;
            height: 2rem;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 4px;
        }

        .close-btn:hover {
            background: #f0f0f0;
            color: #181818;
        }

        /* Task Detail Modal Styles */
        .detail-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1.5rem;
            margin-bottom: 1.5rem;
        }

        .detail-field {
            margin-bottom: 1rem;
        }

        .detail-field.full-width {
            grid-column: 1 / -1;
        }

        .detail-label {
            display: block;
            font-weight: 600;
            color: #3E3E3C;
            font-size: 0.875rem;
            margin-bottom: 0.5rem;
        }

        .detail-input, .detail-select, .detail-textarea {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #D8D8D8;
            border-radius: 4px;
            font-size: 0.875rem;
            background: white;
        }

        .detail-input:focus, .detail-select:focus, .detail-textarea:focus {
            outline: none;
            border-color: #0176D3;
            box-shadow: 0 0 0 2px rgba(1, 118, 211, 0.1);
        }

        .detail-textarea {
            min-height: 100px;
            resize: vertical;
            font-family: inherit;
        }

        /* Remove button for user-added tasks */
        .remove-btn {
            background: #dc2626;
            color: white;
            border: none;
            border-radius: 3px;
            padding: 0.25rem 0.5rem;
            font-size: 0.625rem;
            cursor: pointer;
            transition: background 0.2s ease;
            margin-left: 0.5rem;
        }

        .remove-btn:hover {
            background: #b91c1c;
        }

        .service-name-container {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
    </style>
</head>
<body>
    <!-- Program Header -->
    <div class="program-header">
        <h1 class="program-title">TechCorp Affiliate Program</h1>
    </div>

    <div class="main-container">
        <!-- Left Sidebar: My Packages -->
        <div class="packages-sidebar">
            <div class="packages-header">
                <div style="display: flex; align-items: center; gap: 0.5rem;">
                    <span style="background: #f39c12; width: 20px; height: 20px; border-radius: 3px; display: flex; align-items: center; justify-content: center; font-size: 0.75rem; color: white;">📦</span>
                    <h2 style="font-size: 1rem; font-weight: 600; color: #181818; margin: 0;">My Packages</h2>
                    <button style="background: none; border: none; color: #706E6B; cursor: pointer; font-size: 0.75rem;">▼</button>
                </div>
                <button style="background: none; border: none; color: #706E6B; cursor: pointer; font-size: 1rem;">ℹ️</button>
            </div>
            
            <div class="packages-info">
                <span style="color: #706E6B; font-size: 0.75rem;">4 items • Updated less 3 minutes</span>
            </div>
            
            <div class="packages-search">
                <input type="text" placeholder="Search this list..." style="width: 100%; padding: 0.5rem; border: 1px solid #d8d8d8; border-radius: 4px; font-size: 0.875rem;">
            </div>
            
            <div class="packages-list">
                <div class="package-item">
                    <input type="checkbox" style="margin-right: 0.75rem;">
                    <div>
                        <div class="package-name">Healthcare</div>
                        <div class="package-type">Premium</div>
                    </div>
                </div>
                
                <div class="package-item active">
                    <input type="checkbox" checked style="margin-right: 0.75rem;">
                    <div>
                        <div class="package-name">TechCorp Affiliate Program</div>
                        <div class="package-type">Premium</div>
                    </div>
                </div>
                
                <div class="package-item">
                    <input type="checkbox" style="margin-right: 0.75rem;">
                    <div>
                        <div class="package-name">H&M</div>
                        <div class="package-type">Core</div>
                    </div>
                </div>
                
                <div class="package-item">
                    <input type="checkbox" style="margin-right: 0.75rem;">
                    <div>
                        <div class="package-name">Italian Furniture</div>
                        <div class="package-type">Premium</div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Middle Section: Main Content with Tabs -->
        <div class="left-section">
            <div class="tabs-container">
                <div class="tabs-nav">
                    <button class="tab-button active" data-tab="services">Services (10+)</button>
                    <button class="tab-button" data-tab="tasks">Tasks</button>
                </div>

                <!-- Services Tab -->
                <div id="services-tab" class="tab-content active">
                    <div style="padding: 1.5rem;">
                        <div style="color: #706E6B; font-size: 0.875rem; margin-bottom: 1rem;">10+ items • Updated a few seconds ago</div>
                        
                        <div class="table-container">
                            <table class="service-table">
                                <thead>
                                    <tr>
                                        <th style="width: 5%;">#</th>
                                        <th style="width: 25%;">Service Name</th>
                                        <th style="width: 15%;">Frequency</th>
                                        <th style="width: 15%;">Occurrence</th>
                                        <th style="width: 15%;">Reference Date</th>
                                        <th style="width: 20%;">Included for Client</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr class="task-row">
                                        <td>1</td>
                                        <td><div class="service-name" style="cursor: default; text-decoration: none; color: #181818;">1 hour regular call with Account Contact</div></td>
                                        <td>Weekly</td>
                                        <td>Upon Request</td>
                                        <td>2025-06-05</td>
                                        <td><label style="display: flex; align-items: center; font-size: 0.875rem;"><input type="checkbox" checked disabled style="margin-right: 0.5rem;">Yes</label></td>
                                    </tr>
                                    <tr class="task-row">
                                        <td>2</td>
                                        <td><div class="service-name" style="cursor: default; text-decoration: none; color: #181818;">Business Review</div></td>
                                        <td>Quarterly</td>
                                        <td>Included</td>
                                        <td>2025-06-05</td>
                                        <td><label style="display: flex; align-items: center; font-size: 0.875rem;"><input type="checkbox" checked disabled style="margin-right: 0.5rem;">Yes</label></td>
                                    </tr>
                                    <tr class="task-row">
                                        <td>3</td>
                                        <td><div class="service-name" style="cursor: default; text-decoration: none; color: #181818;">Competitor Benchmark</div></td>
                                        <td>Quarterly</td>
                                        <td>Included</td>
                                        <td>2025-06-05</td>
                                        <td><label style="display: flex; align-items: center; font-size: 0.875rem;"><input type="checkbox" checked disabled style="margin-right: 0.5rem;">Yes</label></td>
                                    </tr>
                                    <tr class="task-row">
                                        <td>4</td>
                                        <td><div class="service-name" style="cursor: default; text-decoration: none; color: #181818;">Gap Analysis</div></td>
                                        <td>Quarterly</td>
                                        <td>Included</td>
                                        <td>2025-06-05</td>
                                        <td><label style="display: flex; align-items: center; font-size: 0.875rem;"><input type="checkbox" checked disabled style="margin-right: 0.5rem;">Yes</label></td>
                                    </tr>
                                    <tr class="task-row">
                                        <td>5</td>
                                        <td><div class="service-name" style="cursor: default; text-decoration: none; color: #181818;">Industry and Network Insight</div></td>
                                        <td>Quarterly</td>
                                        <td>Included</td>
                                        <td>2025-06-05</td>
                                        <td><label style="display: flex; align-items: center; font-size: 0.875rem;"><input type="checkbox" checked disabled style="margin-right: 0.5rem;">Yes</label></td>
                                    </tr>
                                    <tr class="task-row">
                                        <td>6</td>
                                        <td><div class="service-name" style="cursor: default; text-decoration: none; color: #181818;">Publisher Approvals</div></td>
                                        <td>Weekly</td>
                                        <td>Included</td>
                                        <td>2025-06-05</td>
                                        <td><label style="display: flex; align-items: center; font-size: 0.875rem;"><input type="checkbox" checked disabled style="margin-right: 0.5rem;">Yes</label></td>
                                    </tr>
                                    <tr class="task-row">
                                        <td>7</td>
                                        <td><div class="service-name" style="cursor: default; text-decoration: none; color: #181818;">Publisher Recommendations</div></td>
                                        <td>Monthly</td>
                                        <td>Included</td>
                                        <td>2025-06-05</td>
                                        <td><label style="display: flex; align-items: center; font-size: 0.875rem;"><input type="checkbox" checked disabled style="margin-right: 0.5rem;">Yes</label></td>
                                    </tr>
                                    <tr class="task-row">
                                        <td>8</td>
                                        <td><div class="service-name" style="cursor: default; text-decoration: none; color: #181818;">Reporting and Analysis</div></td>
                                        <td>Weekly</td>
                                        <td>Upon Request</td>
                                        <td>2025-06-05</td>
                                        <td><label style="display: flex; align-items: center; font-size: 0.875rem;"><input type="checkbox" checked disabled style="margin-right: 0.5rem;">Yes</label></td>
                                    </tr>
                                    <tr class="task-row">
                                        <td>9</td>
                                        <td><div class="service-name" style="cursor: default; text-decoration: none; color: #181818;">Review of Strategy Roadmaps</div></td>
                                        <td>Monthly</td>
                                        <td>Included</td>
                                        <td>2025-06-05</td>
                                        <td><label style="display: flex; align-items: center; font-size: 0.875rem;"><input type="checkbox" checked disabled style="margin-right: 0.5rem;">Yes</label></td>
                                    </tr>
                                    <tr class="task-row">
                                        <td>10</td>
                                        <td><div class="service-name" style="cursor: default; text-decoration: none; color: #181818;">Strategy Planning and Delivery Call / Meeting</div></td>
                                        <td>Quarterly</td>
                                        <td>Included</td>
                                        <td>2025-06-05</td>
                                        <td><label style="display: flex; align-items: center; font-size: 0.875rem;"><input type="checkbox" checked disabled style="margin-right: 0.5rem;">Yes</label></td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                        
                        <div style="text-align: center; margin-top: 1rem;">
                            <a href="#" style="color: #0176D3; text-decoration: underline; font-size: 0.875rem;">View All</a>
                        </div>
                    </div>
                </div>

                <!-- Tasks Tab -->
                <div id="tasks-tab" class="tab-content">
                    <div class="container" style="box-shadow: none; border-radius: 0;">
                        <div class="header">
                            <h1>Tasks</h1>
                            <button class="btn btn-primary" id="addTaskBtn">+ Add Task</button>
                        </div>
                        
                        <div class="table-container">
                            <table class="service-table">
                                <thead>
                                    <tr>
                                        <th class="col-service">Service Name</th>
                                        <th class="col-date">Due Date</th>
                                        <th class="col-assigned">Assigned To</th>
                                        <th class="col-status">Status</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr class="task-row">
                                        <td><div class="service-name" onclick="openTaskDetail('Performance Reviews', 'Monthly analysis of campaign performance and optimization recommendations', 'Optimization', '2025-06-15', 'Chandler Bing', 'Pending client feedback on Q1 performance metrics', 'not-completed')">Performance Reviews</div></td>
                                        <td><div style="color: #181818; font-size: 0.875rem;">2025-06-15</div></td>
                                        <td><div style="color: #181818; font-size: 0.875rem;">Chandler Bing</div></td>
                                        <td><div style="color: #181818; font-size: 0.875rem;">Not Completed</div></td>
                                    </tr>
                                    <tr class="task-row">
                                        <td><div class="service-name" onclick="openTaskDetail('Publisher Recommendations', 'Monthly publisher outreach and partnership recommendations', 'Publisher Management', '2025-06-20', 'Chandler Bing', 'Research in progress for new tech publishers', 'not-completed')">Publisher Recommendations</div></td>
                                        <td><div style="color: #181818; font-size: 0.875rem;">2025-06-20</div></td>
                                        <td><div style="color: #181818; font-size: 0.875rem;">Chandler Bing</div></td>
                                        <td><div style="color: #181818; font-size: 0.875rem;">Not Completed</div></td>
                                    </tr>
                                    <tr class="task-row">
                                        <td><div class="service-name" onclick="openTaskDetail('Monthly Check-ins', 'Regular client calls to discuss performance and strategy', 'Communication', '2025-06-10', 'Chandler Bing', 'Call went well, client satisfied with current performance', 'completed')">Monthly Check-ins</div></td>
                                        <td><div style="color: #181818; font-size: 0.875rem;">2025-06-10</div></td>
                                        <td><div style="color: #181818; font-size: 0.875rem;">Chandler Bing</div></td>
                                        <td><div style="color: #04844B; font-size: 0.875rem; font-weight: 600;">Completed</div></td>
                                    </tr>
                                    <tr class="task-row">
                                        <td><div class="service-name" onclick="openTaskDetail('Account Maintenance', 'Regular account cleanup and maintenance tasks', 'Housekeeping', '2025-06-25', 'Chandler Bing', 'Scheduled for next week - cleanup inactive publishers', 'not-completed')">Account Maintenance</div></td>
                                        <td><div style="color: #181818; font-size: 0.875rem;">2025-06-25</div></td>
                                        <td><div style="color: #181818; font-size: 0.875rem;">Chandler Bing</div></td>
                                        <td><div style="color: #181818; font-size: 0.875rem;">Not Completed</div></td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Right Section: Program Information with Tabs -->
        <div class="right-section">
            <div class="tabs-container">
                <div class="tabs-nav">
                    <button class="tab-button active" data-tab="program">Program</button>
                    <button class="tab-button" data-tab="package">SLA Board Info</button>
                    <button class="tab-button" data-tab="contacts">Contact Roles</button>
                </div>

                <!-- Program Information Tab -->
                <div id="program-tab" class="tab-content active">
                    <div style="padding: 1.5rem;">
                        <div class="info-section">
                            <div class="info-label">Program</div>
                            <div class="info-value link">TechCorp Affiliate Program</div>
                        </div>
                        <div class="info-section">
                            <div class="info-label">Package</div>
                            <div class="info-value">Premium</div>
                        </div>
                        <div class="info-section">
                            <div class="info-label">Status</div>
                            <div class="info-value status">Active</div>
                        </div>
                        <div class="info-section">
                            <div class="info-label">Account Manager</div>
                            <div class="info-value">Chandler Bing</div>
                        </div>
                        <div class="info-section">
                            <div class="info-label">Awin ID</div>
                            <div class="info-value">12345</div>
                        </div>
                    </div>
                </div>

                <!-- Package Info Tab -->
                <div id="package-tab" class="tab-content">
                    <div style="padding: 1.5rem;">
                        <div class="info-section">
                            <div class="info-label">Package Number</div>
                            <div class="info-value">PKG-2025-001234</div>
                        </div>
                        <div class="info-section">
                            <div class="info-label">Package Type</div>
                            <div class="info-value">Premium</div>
                        </div>
                        <div class="info-section">
                            <div class="info-label">Package Owner</div>
                            <select style="width: 180px; padding: 0.375rem; border: 1px solid #D8D8D8; border-radius: 4px; font-size: 0.75rem; background: white;">
                                <option selected>Chandler Bing</option>
                                <option>Monica Geller</option>
                                <option>Ross Geller</option>
                                <option>Rachel Green</option>
                                <option>Joey Tribbiani</option>
                                <option>Phoebe Buffay</option>
                            </select>
                        </div>
                        <div class="info-section">
                            <div class="info-label">Created Date</div>
                            <div class="info-value">June 5, 2025</div>
                        </div>
                        <div class="info-section">
                            <div class="info-label">Last Modified</div>
                            <div class="info-value">June 25, 2025</div>
                        </div>
                        <div class="info-section">
                            <div class="info-label">Total Services</div>
                            <div class="info-value">10</div>
                        </div>
                    </div>
                </div>

                <!-- Contact Roles Tab -->
                <div id="contacts-tab" class="tab-content">
                    <div style="padding: 1.5rem;">
                        <div class="contact-card">
                            <div class="contact-name">John Smith</div>
                            <div class="contact-detail">
                                <span class="contact-detail-label">Email:</span>
                                <span class="contact-detail-value email">john.smith@test.com</span>
                            </div>
                            <div class="contact-detail">
                                <span class="contact-detail-label">Role:</span>
                                <span class="contact-detail-value">Business (Other)</span>
                            </div>
                            <div class="contact-detail">
                                <span class="contact-detail-label">Survey Recipient:</span>
                                <span class="contact-detail-value">No</span>
                            </div>
                        </div>

                        <div class="contact-card">
                            <div class="contact-name">Alex Johnson</div>
                            <div class="contact-detail">
                                <span class="contact-detail-label">Email:</span>
                                <span class="contact-detail-value email">alex.johnson@test2.com</span>
                            </div>
                            <div class="contact-detail">
                                <span class="contact-detail-label">Role:</span>
                                <span class="contact-detail-value">Business (Other)</span>
                            </div>
                            <div class="contact-detail">
                                <span class="contact-detail-label">Survey Recipient:</span>
                                <span class="contact-detail-value survey-yes">Yes</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Task Detail Modal -->
    <div id="taskDetailModal" class="modal-overlay">
        <div class="modal">
            <div class="modal-header">
                <h2 class="modal-title" id="taskDetailTitle">Task Details</h2>
                <button class="close-btn" id="closeTaskDetailBtn">&times;</button>
            </div>
            <div class="modal-body">
                <div class="detail-grid">
                    <div class="detail-field">
                        <label class="detail-label">Program Name</label>
                        <input type="text" id="taskDetailProgram" class="detail-input" value="TechCorp Affiliate Program" readonly>
                    </div>
                    <div class="detail-field">
                        <label class="detail-label">Package</label>
                        <input type="text" id="taskDetailPackage" class="detail-input" value="Premium" readonly>
                    </div>
                    <div class="detail-field">
                        <label class="detail-label">Service Name</label>
                        <input type="text" id="taskDetailName" class="detail-input" readonly>
                    </div>
                    <div class="detail-field">
                        <label class="detail-label">Category</label>
                        <input type="text" id="taskDetailCategory" class="detail-input" readonly>
                    </div>
                    <div class="detail-field full-width">
                        <label class="detail-label">Service Description</label>
                        <textarea id="taskDetailDescription" class="detail-textarea" readonly></textarea>
                    </div>
                    <div class="detail-field">
                        <label class="detail-label">Due Date</label>
                        <input type="date" id="taskDetailDueDate" class="detail-input">
                    </div>
                    <div class="detail-field">
                        <label class="detail-label">Assigned To</label>
                        <select id="taskDetailAssigned" class="detail-select">
                            <option>Chandler Bing</option>
                            <option>Monica Geller</option>
                            <option>Ross Geller</option>
                            <option>Rachel Green</option>
                            <option>Joey Tribbiani</option>
                            <option>Phoebe Buffay</option>
                        </select>
                    </div>
                    <div class="detail-field">
                        <label class="detail-label">Status</label>
                        <select id="taskDetailStatus" class="detail-select">
                            <option value="not-completed">Not Completed</option>
                            <option value="completed">Completed</option>
                            <option value="skipped">Skipped</option>
                        </select>
                    </div>
                    <div class="detail-field full-width">
                        <label class="detail-label">Notes</label>
                        <textarea id="taskDetailNotes" class="detail-textarea" placeholder="Add notes, comments, or updates about this task..."></textarea>
                    </div>
                </div>
            </div>
            <div class="modal-actions">
                <button class="btn btn-secondary" id="cancelTaskDetailBtn">Cancel</button>
                <button class="btn btn-primary" id="saveTaskDetailBtn">Save Changes</button>
            </div>
        </div>
    </div>

    <!-- Add Task Modal -->
    <div id="addTaskModal" class="modal-overlay">
        <div class="modal">
            <div class="modal-header">
                <h2 class="modal-title">Add New Task</h2>
                <button class="close-btn" id="closeModalBtn">&times;</button>
            </div>
            <div class="modal-body">
                <div class="form-group">
                    <label for="serviceSelect" class="form-label">Select Service</label>
                    <select id="serviceSelect" class="form-select">
                        <option value="">Choose a service...</option>
                        <option value="gap-analysis">Gap Analysis - Quarterly (Occurrence: Included, Included: Yes)</option>
                        <option value="industry-network-insight">Industry and Network Insight - Quarterly (Occurrence: Included, Included: Yes)</option>
                        <option value="1h-regular-call">1 hour regular call with Account Contact - Weekly (Occurrence: Upon Request, Included: Yes)</option>
                        <option value="business-review">Business Review - Quarterly (Occurrence: Included, Included: Yes)</option>
                        <option value="competitor-benchmark">Competitor Benchmark - Quarterly (Occurrence: Included, Included: Yes)</option>
                        <option value="publisher-approvals">Publisher Approvals - Weekly (Occurrence: Included, Included: Yes)</option>
                        <option value="reporting-analysis">Reporting and Analysis - Weekly (Occurrence: Upon Request, Included: Yes)</option>
                        <option value="strategy-roadmaps">Review of Strategy Roadmaps - Monthly (Occurrence: Included, Included: Yes)</option>
                        <option value="strategy-planning">Strategy Planning and Delivery Call / Meeting - Quarterly (Occurrence: Included, Included: Yes)</option>
                        <option value="other-tasks">Other Tasks - Other (Ad-hoc requests)</option>
                    </select>
                </div>

                <!-- Additional fields for Other Tasks (initially hidden) -->
                <div id="otherTaskFields" style="display: none;">
                    <div class="form-group">
                        <label for="taskTitle" class="form-label">Task Title</label>
                        <input type="text" id="taskTitle" class="form-select" placeholder="e.g., Create Black Friday landing page">
                    </div>
                    <div class="form-group">
                        <label for="taskDescription" class="form-label">Task Description</label>
                        <textarea id="taskDescription" class="form-select" rows="3" placeholder="Describe what needs to be done and any specific requirements..."></textarea>
                    </div>
                </div>

                <div class="form-group">
                    <label for="assignedTo" class="form-label">Assigned To</label>
                    <select id="assignedTo" class="form-select">
                        <option selected>Chandler Bing</option>
                        <option>Monica Geller</option>
                        <option>Ross Geller</option>
                        <option>Rachel Green</option>
                        <option>Joey Tribbiani</option>
                        <option>Phoebe Buffay</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="taskDueDate" class="form-label">Due Date</label>
                    <input type="date" id="taskDueDate" class="form-select" value="2025-06-30">
                </div>
                
                <div class="form-group">
                    <label for="taskNotes" class="form-label">Notes</label>
                    <textarea id="taskNotes" class="form-select" rows="3" placeholder="Add any notes, comments, or additional context for this task..."></textarea>
                </div>
            </div>
            <div class="modal-actions">
                <button class="btn btn-secondary" id="cancelAddTaskBtn">Cancel</button>
                <button class="btn btn-primary" id="createTaskBtn">Create Task</button>
            </div>
        </div>
    </div>

    <script>
        // Global variables to store current task data
        let currentTaskData = {};

        // Initialize the application
        document.addEventListener('DOMContentLoaded', function() {
            initializeTabs();
            initializeModals();
            initializeAddTask();
        });

        // Tab functionality
        function initializeTabs() {
            // Main content tabs (Services/Tasks) - Left side
            const leftTabButtons = document.querySelectorAll('.left-section .tabs-nav .tab-button');
            const leftTabContents = document.querySelectorAll('.left-section .tab-content');

            leftTabButtons.forEach(button => {
                button.addEventListener('click', function() {
                    const targetTab = this.getAttribute('data-tab');
                    
                    // Remove active class from left tab buttons and contents
                    leftTabButtons.forEach(btn => btn.classList.remove('active'));
                    leftTabContents.forEach(content => content.classList.remove('active'));
                    
                    // Add active class to clicked button and corresponding content
                    this.classList.add('active');
                    document.getElementById(targetTab + '-tab').classList.add('active');
                });
            });

            // Right sidebar tabs (Program/Package Info/Contact Roles)
            const rightTabButtons = document.querySelectorAll('.right-section .tabs-nav .tab-button');
            const rightTabContents = document.querySelectorAll('.right-section .tab-content');

            rightTabButtons.forEach(button => {
                button.addEventListener('click', function() {
                    const targetTab = this.getAttribute('data-tab');
                    
                    // Remove active class from right tab buttons and contents
                    rightTabButtons.forEach(btn => btn.classList.remove('active'));
                    rightTabContents.forEach(content => content.classList.remove('active'));
                    
                    // Add active class to clicked button and corresponding content
                    this.classList.add('active');
                    document.getElementById(targetTab + '-tab').classList.add('active');
                });
            });
        }

        // Modal functionality
        function initializeModals() {
            // Add Task Modal
            const addTaskBtn = document.getElementById('addTaskBtn');
            const addTaskModal = document.getElementById('addTaskModal');
            const closeModalBtn = document.getElementById('closeModalBtn');
            const cancelAddTaskBtn = document.getElementById('cancelAddTaskBtn');

            if (addTaskBtn) {
                addTaskBtn.addEventListener('click', () => {
                    addTaskModal.style.display = 'block';
                });
            }

            if (closeModalBtn) {
                closeModalBtn.addEventListener('click', () => {
                    addTaskModal.style.display = 'none';
                });
            }

            if (cancelAddTaskBtn) {
                cancelAddTaskBtn.addEventListener('click', () => {
                    addTaskModal.style.display = 'none';
                });
            }

            // Task Detail Modal
            const taskDetailModal = document.getElementById('taskDetailModal');
            const closeTaskDetailBtn = document.getElementById('closeTaskDetailBtn');
            const cancelTaskDetailBtn = document.getElementById('cancelTaskDetailBtn');
            const saveTaskDetailBtn = document.getElementById('saveTaskDetailBtn');

            if (closeTaskDetailBtn) {
                closeTaskDetailBtn.addEventListener('click', () => {
                    taskDetailModal.style.display = 'none';
                });
            }

            if (cancelTaskDetailBtn) {
                cancelTaskDetailBtn.addEventListener('click', () => {
                    taskDetailModal.style.display = 'none';
                });
            }

            if (saveTaskDetailBtn) {
                saveTaskDetailBtn.addEventListener('click', () => {
                    saveTaskDetails();
                });
            }

            // Close modals when clicking outside
            window.addEventListener('click', (e) => {
                if (e.target === addTaskModal) {
                    addTaskModal.style.display = 'none';
                }
                if (e.target === taskDetailModal) {
                    taskDetailModal.style.display = 'none';
                }
            });
        }

        // Open task detail modal
        function openTaskDetail(name, description, category, dueDate, assignedTo, notes, status) {
            // Store current task data
            currentTaskData = {
                name: name,
                description: description,
                category: category,
                dueDate: dueDate,
                assignedTo: assignedTo,
                notes: notes,
                status: status
            };

            // Populate the modal fields
            document.getElementById('taskDetailTitle').textContent = name;
            document.getElementById('taskDetailProgram').value = 'TechCorp Affiliate Program';
            document.getElementById('taskDetailPackage').value = 'Premium';
            document.getElementById('taskDetailName').value = name;
            document.getElementById('taskDetailDescription').value = description;
            document.getElementById('taskDetailCategory').value = category;
            document.getElementById('taskDetailDueDate').value = dueDate;
            document.getElementById('taskDetailNotes').value = notes;
            
            // Set the assigned person
            const assignedSelect = document.getElementById('taskDetailAssigned');
            if (assignedSelect) {
                assignedSelect.value = assignedTo;
            }

            // Set the status
            const statusSelect = document.getElementById('taskDetailStatus');
            if (statusSelect) {
                statusSelect.value = status;
            }

            // Show the modal
            document.getElementById('taskDetailModal').style.display = 'block';
        }

        // Save task details
        function saveTaskDetails() {
            const updatedData = {
                name: document.getElementById('taskDetailName').value,
                description: document.getElementById('taskDetailDescription').value,
                category: document.getElementById('taskDetailCategory').value,
                dueDate: document.getElementById('taskDetailDueDate').value,
                assignedTo: document.getElementById('taskDetailAssigned').value,
                notes: document.getElementById('taskDetailNotes').value,
                status: document.getElementById('taskDetailStatus').value
            };

            // Find the task row in the table and update it
            const serviceNameElements = document.querySelectorAll('.service-name');
            let targetRow = null;
            
            serviceNameElements.forEach(element => {
                if (element.textContent.trim() === currentTaskData.name) {
                    targetRow = element.closest('tr');
                }
            });

            if (targetRow) {
                // Update the row cells
                const cells = targetRow.querySelectorAll('td');
                
                // Update due date (2nd cell)
                cells[1].innerHTML = `<div style="color: #181818; font-size: 0.875rem;">${updatedData.dueDate}</div>`;
                
                // Update assigned to (3rd cell)
                cells[2].innerHTML = `<div style="color: #181818; font-size: 0.875rem;">${updatedData.assignedTo}</div>`;
                
                // Update status (4th cell) with appropriate styling
                let statusColor = '#181818';
                let statusWeight = 'normal';
                if (updatedData.status === 'completed') {
                    statusColor = '#04844B';
                    statusWeight = '600';
                } else if (updatedData.status === 'skipped') {
                    statusColor = '#FF6B35';
                    statusWeight = '600';
                }
                
                const statusText = updatedData.status === 'not-completed' ? 'Not Completed' : 
                                 updatedData.status === 'completed' ? 'Completed' : 'Skipped';
                
                cells[3].innerHTML = `<div style="color: ${statusColor}; font-size: 0.875rem; font-weight: ${statusWeight};">${statusText}</div>`;
                
                // Update the onclick handler with new data
                const serviceNameElement = cells[0].querySelector('.service-name');
                if (serviceNameElement) {
                    serviceNameElement.setAttribute('onclick', 
                        `openTaskDetail('${updatedData.name}', '${updatedData.description}', '${updatedData.category}', '${updatedData.dueDate}', '${updatedData.assignedTo}', '${updatedData.notes}', '${updatedData.status}')`
                    );
                }
            }

            // Update the current task data
            currentTaskData = updatedData;

            // Show success message
            alert('Task details saved successfully!');
            
            // Close the modal
            document.getElementById('taskDetailModal').style.display = 'none';
        }

        // Remove task function
        function removeTask(button) {
            if (confirm('Are you sure you want to remove this task?')) {
                const row = button.closest('tr');
                if (row) {
                    row.remove();
                }
            }
        }

        // Add task functionality
        function initializeAddTask() {
            const createTaskBtn = document.getElementById('createTaskBtn');
            const serviceSelect = document.getElementById('serviceSelect');
            const otherTaskFields = document.getElementById('otherTaskFields');

            // Show/hide other task fields based on selection
            if (serviceSelect) {
                serviceSelect.addEventListener('change', function() {
                    if (this.value === 'other-tasks') {
                        otherTaskFields.style.display = 'block';
                    } else {
                        otherTaskFields.style.display = 'none';
                    }
                });
            }

            // Create task button click handler
            if (createTaskBtn) {
                createTaskBtn.addEventListener('click', function() {
                    createNewTask();
                });
            }
        }

        // Create new task function
        function createNewTask() {
            const serviceSelect = document.getElementById('serviceSelect');
            const assignedTo = document.getElementById('assignedTo');
            const taskDueDate = document.getElementById('taskDueDate');
            const taskNotes = document.getElementById('taskNotes');
            const taskTitle = document.getElementById('taskTitle');
            const taskDescription = document.getElementById('taskDescription');

            // Validate required fields
            if (!serviceSelect.value) {
                alert('Please select a service');
                return;
            }

            // Get task data based on selection
            let taskData = {};
            
            if (serviceSelect.value === 'other-tasks') {
                // Custom task
                if (!taskTitle.value.trim()) {
                    alert('Please enter a task title');
                    return;
                }
                taskData = {
                    name: taskTitle.value.trim(),
                    description: taskDescription.value.trim() || 'Custom task - no description provided',
                    category: 'Other',
                    isCustom: true
                };
            } else {
                // Predefined service
                const serviceData = getServiceData(serviceSelect.value);
                taskData = {
                    name: serviceData.name,
                    description: serviceData.description,
                    category: serviceData.category,
                    isCustom: false
                };
            }

            // Create the new row
            const tableBody = document.querySelector('#tasks-tab .service-table tbody');
            const newRow = document.createElement('tr');
            newRow.className = 'task-row';

            const taskNameHtml = taskData.isCustom 
                ? `<div class="service-name-container">
                     <div class="service-name" onclick="openTaskDetail('${taskData.name}', '${taskData.description}', '${taskData.category}', '${taskDueDate.value}', '${assignedTo.value}', '${taskNotes.value}', 'not-completed')">${taskData.name}</div>
                     <button class="remove-btn" onclick="removeTask(this)">Delete</button>
                   </div>`
                : `<div class="service-name" onclick="openTaskDetail('${taskData.name}', '${taskData.description}', '${taskData.category}', '${taskDueDate.value}', '${assignedTo.value}', '${taskNotes.value}', 'not-completed')">${taskData.name}</div>`;

            newRow.innerHTML = `
                <td>${taskNameHtml}</td>
                <td>
                    <div style="color: #181818; font-size: 0.875rem;">${taskDueDate.value}</div>
                </td>
                <td>
                    <div style="color: #181818; font-size: 0.875rem;">${assignedTo.value}</div>
                </td>
                <td>
                    <div style="color: #181818; font-size: 0.875rem;">Not Completed</div>
                </td>
            `;

            // Add the row to the table
            tableBody.appendChild(newRow);

            // Clear the form and close modal
            clearAddTaskForm();
            document.getElementById('addTaskModal').style.display = 'none';

            // Show success message
            alert('Task added successfully!');
        }

        // Get service data based on selection
        function getServiceData(serviceValue) {
            const serviceMap = {
                'gap-analysis': {
                    name: 'Gap Analysis',
                    description: 'Identify gaps in program performance and provide recommendations for improvement',
                    category: 'Analysis'
                },
                'industry-network-insight': {
                    name: 'Industry and Network Insight',
                    description: 'Quarterly industry trends and network insights to inform strategy',
                    category: 'Strategic Planning'
                },
                '1h-regular-call': {
                    name: '1 hour regular call with Account Contact',
                    description: 'Regular client communication call to discuss performance and updates',
                    category: 'Communication'
                },
                'business-review': {
                    name: 'Business Review',
                    description: 'Quarterly business performance review and strategic assessment',
                    category: 'Analysis'
                },
                'competitor-benchmark': {
                    name: 'Competitor Benchmark',
                    description: 'Monthly competitor analysis and benchmarking against industry standards',
                    category: 'Analysis'
                },
                'publisher-approvals': {
                    name: 'Publisher Approvals',
                    description: 'Weekly publisher approval process and partner management',
                    category: 'Publisher Management'
                },
                'reporting-analysis': {
                    name: 'Reporting and Analysis',
                    description: 'Weekly performance reporting and analysis of key metrics',
                    category: 'Optimization'
                },
                'strategy-roadmaps': {
                    name: 'Review of Strategy Roadmaps',
                    description: 'Monthly review of strategic roadmaps and planning initiatives',
                    category: 'Strategic Planning'
                },
                'strategy-planning': {
                    name: 'Strategy Planning and Delivery Call / Meeting',
                    description: 'Quarterly strategic planning sessions and delivery discussions',
                    category: 'Strategic Planning'
                }
            };
            return serviceMap[serviceValue] || { name: 'Unknown Service', description: '', category: 'Other' };
        }

        // Clear add task form
        function clearAddTaskForm() {
            document.getElementById('serviceSelect').value = '';
            document.getElementById('taskTitle').value = '';
            document.getElementById('taskDescription').value = '';
            document.getElementById('assignedTo').selectedIndex = 0;
            document.getElementById('taskDueDate').value = '2025-06-30';
            document.getElementById('taskNotes').value = '';
            document.getElementById('otherTaskFields').style.display = 'none';
        }

        // Open service detail modal (placeholder for now)
        function openServiceDetail(name, description, frequency, executionType, referenceDate, owner, included) {
            alert(`Service Details:\nName: ${name}\nDescription: ${description}\nFrequency: ${frequency}\nExecution Type: ${executionType}\nReference Date: ${referenceDate}\nIncluded: ${included ? 'Yes' : 'No'}`);
        }
    </script>
</body>
</html>
                            
