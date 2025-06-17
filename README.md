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
            max-width: 1400px;
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
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            gap: 1.5rem;
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

        .service-description {
            font-size: 0.75rem;
            color: #706E6B;
            line-height: 1.4;
            margin-top: 0.25rem;
        }

        .category {
            font-size: 0.75rem;
            color: #181818;
        }

        .date-field {
            background: white;
            border: 1px solid #D8D8D8;
            border-radius: 4px;
            padding: 0.5rem;
            font-size: 0.875rem;
            font-family: inherit;
            width: 130px;
        }

        .select-field {
            background: white;
            border: 1px solid #D8D8D8;
            border-radius: 4px;
            padding: 0.5rem;
            font-size: 0.875rem;
            min-width: 120px;
            cursor: pointer;
        }

        .select-field:focus, .date-field:focus {
            outline: none;
            border-color: #0176D3;
        }

        .col-service { width: 22%; }
        .col-description { width: 28%; }
        .col-category { width: 10%; }
        .col-date { width: 12%; }
        .col-assigned { width: 16%; }
        .col-status { width: 12%; }

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
            padding: 1.5rem;
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
            color: #04844B;
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

        .modal-subtitle {
            font-size: 0.875rem;
            color: #706E6B;
            margin: 0.5rem 0 0 0;
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
        <div style="display: flex; justify-content: space-between; align-items: center;">
            <h1 class="program-title">TechCorp Affiliate Program</h1>
            <button class="btn btn-primary" id="addTaskBtn">+ Add Task</button>
        </div>
    </div>

    <div class="main-container">
        <!-- Left Section: Service Tasks Table -->
        <div class="left-section">
            <div class="container">
                <div class="header">
                    <h1>Service Tasks</h1>
                </div>
                
                <div class="table-container">
                    <table class="service-table">
                        <thead>
                            <tr>
                                <th class="col-service">Service Name</th>
                                <th class="col-description">Description</th>
                                <th class="col-category">Category</th>
                                <th class="col-date">Due Date</th>
                                <th class="col-assigned">Assigned To</th>
                                <th class="col-status">Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr class="task-row">
                                <td>
                                    <div class="service-name" onclick="openTaskDetail('Performance Reviews', 'Monthly analysis of campaign performance and optimization recommendations', 'Optimization', '2025-06-15', 'Chandler Bing', 'Pending client feedback on Q1 performance metrics', 'not-completed')">Performance Reviews</div>
                                </td>
                                <td>
                                    <div class="service-description">Monthly analysis of campaign performance and optimization recommendations</div>
                                </td>
                                <td>
                                    <div class="category">Optimization</div>
                                </td>
                                <td>
                                    <input type="date" class="date-field" value="2025-06-15">
                                </td>
                                <td>
                                    <select class="select-field">
                                        <option selected>Chandler Bing</option>
                                        <option>Monica Geller</option>
                                        <option>Ross Geller</option>
                                        <option>Rachel Green</option>
                                        <option>Joey Tribbiani</option>
                                        <option>Phoebe Buffay</option>
                                    </select>
                                </td>
                                <td>
                                    <select class="select-field" style="width: 100px; font-size: 0.75rem;">
                                        <option value="not-completed">Not Completed</option>
                                        <option value="completed">Completed</option>
                                    </select>
                                </td>
                            </tr>
                            
                            <tr class="task-row">
                                <td>
                                    <div class="service-name" onclick="openTaskDetail('Publisher Recommendations', 'Monthly publisher outreach and partnership recommendations', 'Publisher Management', '2025-06-20', 'Chandler Bing', 'Research in progress for new tech publishers', 'not-completed')">Publisher Recommendations</div>
                                </td>
                                <td>
                                    <div class="service-description">Monthly publisher outreach and partnership recommendations</div>
                                </td>
                                <td>
                                    <div class="category">Publisher Management</div>
                                </td>
                                <td>
                                    <input type="date" class="date-field" value="2025-06-20">
                                </td>
                                <td>
                                    <select class="select-field">
                                        <option selected>Chandler Bing</option>
                                        <option>Monica Geller</option>
                                        <option>Ross Geller</option>
                                        <option>Rachel Green</option>
                                        <option>Joey Tribbiani</option>
                                        <option>Phoebe Buffay</option>
                                    </select>
                                </td>
                                <td>
                                    <select class="select-field" style="width: 100px; font-size: 0.75rem;">
                                        <option value="not-completed">Not Completed</option>
                                        <option value="completed">Completed</option>
                                    </select>
                                </td>
                            </tr>
                            
                            <tr class="task-row">
                                <td>
                                    <div class="service-name" onclick="openTaskDetail('Monthly Check-ins', 'Regular client calls to discuss performance and strategy', 'Communication', '2025-06-10', 'Chandler Bing', 'Call went well, client satisfied with current performance', 'completed')">Monthly Check-ins</div>
                                </td>
                                <td>
                                    <div class="service-description">Regular client calls to discuss performance and strategy</div>
                                </td>
                                <td>
                                    <div class="category">Communication</div>
                                </td>
                                <td>
                                    <input type="date" class="date-field" value="2025-06-10">
                                </td>
                                <td>
                                    <select class="select-field">
                                        <option selected>Chandler Bing</option>
                                        <option>Monica Geller</option>
                                        <option>Ross Geller</option>
                                        <option>Rachel Green</option>
                                        <option>Joey Tribbiani</option>
                                        <option>Phoebe Buffay</option>
                                    </select>
                                </td>
                                <td>
                                    <select class="select-field" style="width: 100px; font-size: 0.75rem;">
                                        <option value="not-completed">Not Completed</option>
                                        <option value="completed" selected>Completed</option>
                                    </select>
                                </td>
                            </tr>
                            
                            <tr class="task-row">
                                <td>
                                    <div class="service-name" onclick="openTaskDetail('Account Maintenance', 'Regular account cleanup and maintenance tasks', 'Housekeeping', '2025-06-25', 'Chandler Bing', 'Scheduled for next week - cleanup inactive publishers', 'not-completed')">Account Maintenance</div>
                                </td>
                                <td>
                                    <div class="service-description">Regular account cleanup and maintenance tasks</div>
                                </td>
                                <td>
                                    <div class="category">Housekeeping</div>
                                </td>
                                <td>
                                    <input type="date" class="date-field" value="2025-06-25">
                                </td>
                                <td>
                                    <select class="select-field">
                                        <option selected>Chandler Bing</option>
                                        <option>Monica Geller</option>
                                        <option>Ross Geller</option>
                                        <option>Rachel Green</option>
                                        <option>Joey Tribbiani</option>
                                        <option>Phoebe Buffay</option>
                                    </select>
                                </td>
                                <td>
                                    <select class="select-field" style="width: 100px; font-size: 0.75rem;">
                                        <option value="not-completed">Not Completed</option>
                                        <option value="completed">Completed</option>
                                    </select>
                                </td>
                            </tr>
                            
                            <tr class="task-row">
                                <td>
                                    <div class="service-name" onclick="openTaskDetail('Custom: Social Media Audit', 'Quarterly review of social media performance and recommendations', 'Other', '2025-06-18', 'Chandler Bing', 'Awaiting social media access from client', 'not-completed')">Custom: Social Media Audit</div>
                                </td>
                                <td>
                                    <div class="service-description">Quarterly review of social media performance and recommendations</div>
                                </td>
                                <td>
                                    <div class="category">Other</div>
                                </td>
                                <td>
                                    <input type="date" class="date-field" value="2025-06-18">
                                </td>
                                <td>
                                    <select class="select-field">
                                        <option selected>Chandler Bing</option>
                                        <option>Monica Geller</option>
                                        <option>Ross Geller</option>
                                        <option>Rachel Green</option>
                                        <option>Joey Tribbiani</option>
                                        <option>Phoebe Buffay</option>
                                    </select>
                                </td>
                                <td>
                                    <select class="select-field" style="width: 100px; font-size: 0.75rem;">
                                        <option value="not-completed">Not Completed</option>
                                        <option value="completed">Completed</option>
                                    </select>
                                </td>
                            </tr>
                            
                            <tr class="task-row">
                                <td>
                                    <div class="service-name-container">
                                        <div class="service-name" onclick="openTaskDetail('Other Tasks', 'Ad-hoc tasks and client requests not covered by standard services', 'Other', '2025-06-20', 'Chandler Bing', 'No current tasks - ready for ad-hoc requests', 'not-completed')">Other Tasks</div>
                                        <button class="remove-btn" onclick="removeTask(this)" style="display: none;">Delete</button>
                                    </div>
                                </td>
                                <td>
                                    <div class="service-description">Ad-hoc tasks and client requests not covered by standard services</div>
                                </td>
                                <td>
                                    <div class="category">Other</div>
                                </td>
                                <td>
                                    <input type="date" class="date-field" value="2025-06-20">
                                </td>
                                <td>
                                    <select class="select-field">
                                        <option selected>Chandler Bing</option>
                                        <option>Monica Geller</option>
                                        <option>Ross Geller</option>
                                        <option>Rachel Green</option>
                                        <option>Joey Tribbiani</option>
                                        <option>Phoebe Buffay</option>
                                    </select>
                                </td>
                                <td>
                                    <select class="select-field" style="width: 100px; font-size: 0.75rem;">
                                        <option value="not-completed">Not Completed</option>
                                        <option value="completed">Completed</option>
                                    </select>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- Right Section: Tabs -->
        <div class="right-section">
            <div class="tabs-container">
                <div class="tabs-nav">
                    <button class="tab-button active" data-tab="program">Program</button>
                    <button class="tab-button" data-tab="contacts">Contact Roles</button>
                </div>

                <!-- Program Information Tab -->
                <div id="program-tab" class="tab-content active">
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

                <!-- Contact Roles Tab -->
                <div id="contacts-tab" class="tab-content">
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
                        <option value="performance-reviews">Performance Reviews - Optimization</option>
                        <option value="publisher-recommendations">Publisher Recommendations - Publisher Management</option>
                        <option value="monthly-checkins">Monthly Check-ins - Communication</option>
                        <option value="account-maintenance">Account Maintenance - Housekeeping</option>
                        <option value="social-media-audit">Custom: Social Media Audit - Other</option>
                        <option value="other-tasks">Other Tasks - Other (Ad-hoc requests)</option>
                    </select>
                    <div style="font-size: 0.75rem; color: #706E6B; margin-top: 0.5rem;">
                        * Only services configured as "Upon Request" are available for task creation
                    </div>
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
                    <textarea id="taskNotes" class="form-select" rows="3" placeholder="Add any notes, comments, or additional context for this
