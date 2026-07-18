# Connection Guide: Secure Remote Access via Tailscale

## Objective
Establish a secure, WireGuard-based VPN tunnel to access the `proliant` server within the team's private network, without exposing any ports to the public internet.

## Prerequisites
* An active [Tailscale](https://tailscale.com/) account.
* An invitation link provided by the network administrator.

## Step 1: Client Installation
Download and install the appropriate binary for the end-user's operating system.

* **Windows / macOS:** Download the official installer from [tailscale.com/download](https://tailscale.com/download).
* **Linux (Debian/Ubuntu):**
  ```bash ```
    curl -fsSL https://tailscale.com/install.sh | sh
 
## Step 2: Authentication and Invitation
To join a shared network, the user must follow the identity workflow:

* **Accept Invitation:** Access the "Share" link sent by the administrator.
* **Login:** Authenticate using an identity provider (GitHub, Google, Microsoft, etc.).
* **Authorization:** Once the invitation is accepted in the panel, the Tailscale client will detect the new available node.

## Step 3: Connectivity Verification
Once authenticated, validate that the tunnel is correctly established:

* **Check Status:** Run the following command to check the connection status:
  ```bash
  tailscale status
  ```

* **Identify IP:** Locate the internal IP assigned to the `proliant` server. This IP will always follow the `100.x.y.z` format.

* **Validate Route:** Attempt to ping the obtained IP:
  ```bash
  ping 100.x.y.z
  ```
## Step 4: Web Service Access
With the connection established, the Nginx service running on `proliant` is transparently accessible:

* **Access URL:** Open a web browser and navigate to `http://100.x.y.z` (replacing with the corresponding private IP).
* **Security Note:** Since this is a private network, all traffic between the local machine and the `proliant` server is encrypted point-to-point, preventing interception attacks and public port scanning.

## Engineer's Notes (Best Practices)
* **Security:** Keep the Tailscale application updated at all times to receive security patches for the WireGuard protocol.
* **Troubleshooting:** If the connection fails, execute `tailscale up` to force the reconnection of network services.
* **Privacy:** This configuration only grants access to the specific shared device (`proliant`), not to other devices on the administrator's private network.