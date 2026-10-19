# Vacation Tracking System (VTS)

## 1. Problem Domain

It is not uncommon for employees to divide their time across multiple projects and report to multiple project managers. As a result, managers have fewer informal interactions with their employees and find it increasingly difficult to monitor and manage their employees' vacation time.

The Vacation Tracking System (VTS) aims to address this challenge by providing a centralized system for managing employee vacation requests and leave balances.

## 2. Vision

The Vacation Tracking System (VTS) will provide employees with the capability to manage their own vacation time, sick leave, and personal time off without requiring them to be experts in company policies or local facility leave policies.

## 3. Actors

The system interacts with the following actors and external systems:

1. **Employee** — Submits and manages vacation requests.
2. **Managers** — Review vacation requests, approve or reject them, and award personal leave time.
3. **HR Personnel** — Manage employee leave-related information and override restricted actions when necessary.
4. **System Administration Personnel** — Manage system operations and override restricted actions when necessary.
5. **Other Internal Systems** — Retrieve employee vacation request summaries through the system's Web service interface.
6. **HR Department Legacy Systems** — Provide employee information and updates required by the VTS.

## 4. Constraints

1. The system must use existing hardware and middleware.
2. The system must be implemented as an extension of the existing intranet portal.
3. The system must use the portal's Single Sign-On (SSO) mechanisms for authentication.

## 5. Non-Functional Requirements

1. **Usability:** The system must be easy to use.

## 6. Functional Requirements

1. **Vacation Request History and Planning:** The system must provide access to vacation requests from the previous calendar year and allow requests to be made up to one and a half years into the future.
2. **Email Notifications:** The system must send email notifications to request manager approval and notify employees when their request statuses change.
3. **Activity Logging:** The system must maintain activity logs for all transactions.
4. **Administrative Overrides:** HR and system administration personnel must be able to override actions restricted by system rules. All overrides must be logged.
5. **Personal Leave Awards:** Managers must be able to award personal leave time directly, subject to system-defined limits.
6. **Web Service Interface:** The system must provide a Web service interface that allows other internal systems to retrieve an individual employee's vacation request summary.
7. **HR Legacy System Integration:** The system must interface with the HR department's legacy systems to retrieve required employee information and updates.

## 7. Pseudocode

### 7.1 Submit Vacation Request

```text
function String submitVacationRequest(
    VacationRequestDto request,
    EmployeeId empId
) {
    if (!request is valid)
        return "request not valid";

    addRequest(request, empId);

    return "request submitted with pending status";
}
```


### 7.2 Update Vacation Request Status

```text
function void updateRequestStatus(
    RequestId requestId,
    VacationStatus newStatus
) {
    VacationRequest request =
        findByVacationRequestId(requestId)
            .orElseThrow("request not found");

    request.status = newStatus;

    addRequest(request);
}
```
