 (cd "$(git rev-parse --show-toplevel)" && git apply --3way <<'EOF' 
diff --git a//dev/null b/docs/TerminalOperations.md
index 0000000000000000000000000000000000000000..562b62bb4fe58cf83106483a07bb87771f8bd5ff 100644
--- a//dev/null
+++ b/docs/TerminalOperations.md
@@ -0,0 +1,25 @@
+# Terminal Operations Overview
+
+## User Interactions in Terminal Views
+- **NextCall.cshtml**: displays current ticket, allows saving notes, and exposes patient details.
+- **ParkTicket.cshtml**: confirms a ticket is parked and clears current ticket context.
+- **CallFromPark.cshtml**: recalls a parked ticket and reopens patient details.
+- **ServiceTransferList.cshtml**: shows available segments and triggers transfer or direct transfer actions.
+
+## SignalR Endpoints & jQuery Utilities
+- Connects to SignalR hub at `http://localhost/SignalR` and listens for ticket events.
+- Client handlers react to commands like `TicketCalled`, `LoadBrokenTicket`, `TransferredTerminal`, `TransferredService`, and `PrintTicket`.
+- Utility functions perform actions:
+  - `NextCall()` closes the current ticket then requests the next one.
+  - `Park()`, `CallFromPark()`, and `DirectTransferFromPark()` manage parking flow.
+  - `ServiceTransfer()` moves tickets between services; `ServiceTransferList()` fetches options.
+  - `CloseTicket()`, `NoShowTicket()`, `Recall()`, and `BreakCall()` handle ticket lifecycle.
+  - `WaitingList()`, `ParkList()`, `GenerateTicketInfo()` keep UI lists current.
+  - `GenerateTicket()`, `SaveNewPhone()`, `SaveTicketNote()`, and `MoreInformation()` manage customer data.
+
+## Backend API Endpoints
+The client expects backend routes under `/Terminal/` or SignalR methods to support terminal operations:
+- Ticket lifecycle: `NextCall`, `CloseTicket`, `ParkTicket`, `CallFromPark`, `NoShowTicket`, `ServiceTransfer`, `DirectTransferFromPark`.
+- Queue displays: `WaitingList`, `ParkList`, `InfoBox`, `InfoBoxGenerateTicket`, `CheckMacroForReflesh`.
+- Customer management: `GenerateTicket`, `ChangeCustomerPhone`, `SaveNewPhone`, `SaveTicketNote`, `MoreInformation`, `FindCustomer`, `ProcessAssignCustomer`.
+- SignalR server methods: `TerminalOnline`, `ChangeStatus`, `TicketCalled`, `FlashNumber`, `LoadBrokenTicket`.
 
EOF
)
