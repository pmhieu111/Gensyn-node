Gensyn Testnet Node Guide
This guide walks you through setting up and running a Gensyn Testnet node using a rented GPU from Vast.ai.
System Requirements
![image](https://github.com/user-attachments/assets/815ae532-529e-4176-be37-3605b85ad384)
Setup Instructions
1. Sign Up on Vast.ai
Visit cloud.vast.ai.

Create an account.

2. Rent a GPU
Go to the Template section.

Select Nvidia CUDA (Ubuntu).

Rent an RTX 3090 GPU (recommended).
Tip: Pair with a powerful CPU like i9 or AMD Ryzen Threadripper for better performance.

Navigate to the Instances section to verify your rented GPU.

3. Generate SSH Keys
Open Termius (or your preferred SSH client).

Go to Keychain > Key > Generate key.

Set a name for the key.

Select RSA as the key type.

Click Generate & Save.

Copy the generated public key.

4. Add SSH Key to Vast.ai
On the Vast.ai website, go to Settings.

Add the SSH public key copied from Step 3.

Go to Instances.

Click the Key icon next to your instance.

Copy the Direct SSH command.

5. Connect to the GPU
In Termius, paste the Direct SSH command from Step 4 into the search bar.

Click Continue and Save.

Click Add and Continue.

Select Vast as the host.

Click Continue and Save to connect.

6. Get Ngrok Auth Token
Visit dashboard.ngrok.com/get-started/your-authtoken.

Sign up using Gmail or GitHub.

Click Create Account.

Go to Your Auth Token.

Copy and save your Ngrok Auth Token.

7. Get Hugging Face Auth Token
Visit huggingface.co/settings/tokens.

Sign up with your email and fill in the required details.

Click Create Account.

Go to Create New Token.

Set a name for the token.

Click Create Token.

Copy and save the Hugging Face Auth Token.

Running the Node
8. Install sudo

`apt update && apt install -y sudo`

9. Install Dependencies

`sudo apt update && sudo apt install -y python3 python3-venv python3-pip curl wget screen git lsof && \
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - && \
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && \
sudo apt update && sudo apt install -y yarn`

10. Install Node.js

`curl -sSL https://raw.githubusercontent.com/zunxbt/installation/main/node.sh | bash`

11. Clone the Repository

`cd $HOME && [ -d rl-swarm ] && rm -rf rl-swarm; \
git clone https://github.com/zunxbt/rl-swarm.git && cd rl-swarm`

12. Create a Screen Session

`screen -S gensyn`

13. Uninstall Old protobuf

`pip uninstall protobuf -y`

14. Install Compatible protobuf

`pip install "protobuf>=3.12.2,<5.28.0"`

15. Run the Swarm

`python3 -m venv .venv && . .venv/bin/activate && ./run_rl_swarm.sh`

Enter the Ngrok Auth Token from Step 6 when prompted.

Note the website URL displayed in the terminal.

16. Log In
Open the URL from Step 15 in your browser.

Click Visit Site > Login.

Enter your email and click Continue.

Verify your email as prompted.

17. Set Hugging Face Auth Token
When prompted with Y/N, enter Y.

Enter the Hugging Face Auth Token from Step 7.

Wait approximately 10 minutes for the node to initialize.

Detach from the screen session by pressing Ctrl + A + D.

18. Check Your Points
Note your node name from the terminal.

Visit dashboard.gensyn.ai/api/leaderboard-cumulative.

Use Ctrl + F to search for your node name.

19. Final Steps
Reattach to the screen session to check logs:

```screen -r```

Note: Only the top 100 nodes appear on the leaderboard. Don’t worry if your node isn’t listed.

Backup the swarm.pem file:
Use SFTP to transfer swarm.pem from the rl-swarm directory to your local machine.

Stay tuned for updates on when to stop the node (not intended to run long-term).

Additional Notes
Execute all commands one-by-one as listed.

Keep your Ngrok and Hugging Face tokens secure.

If you encounter issues, check the logs using screen -r.

