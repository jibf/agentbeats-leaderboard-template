# Multi-Benchmark Green Agent Leaderboard

> Comprehensive evaluation leaderboard for BFCL, ComplexFuncBench (CFB), and Tau2 benchmarks

This leaderboard evaluates purple agents (LLM-powered function calling agents) across three industry-standard benchmarks:
- **BFCL (Berkeley Function Calling Leaderboard)**: Tests function calling accuracy
- **ComplexFuncBench (CFB)**: Evaluates multi-turn function calling in travel planning scenarios
- **Tau2**: Assesses customer service conversation capabilities

## About This Green Agent

This green agent provides:
- **Three benchmark modes**: BFCL, CFB, and Tau2
- **Comprehensive metrics**: Accuracy, success rate, call accuracy, pass rate, and domain-specific breakdowns
- **Quality filtering**: Removes known problematic test cases for fair evaluation
- **State isolation**: Ensures independent task evaluation

### Scoring & Evaluation

**BFCL:**
- Accuracy: Percentage of correct function calls using AST-based comparison
- Category breakdown: Performance across different test categories (simple, multi-turn, parallel, etc.)

**ComplexFuncBench:**
- Overall Success Rate: Percentage of successfully completed tasks
- Call Accuracy: Correctness of individual function calls
- Domain-specific stats: Performance by domain (Car-Rental, Hotel, Restaurant, etc.)

**Tau2:**
- Pass Rate: Percentage of passed conversations
- Score: Task completion score out of max possible
- Domain-specific performance: Airline, retail, telecom metrics

## Submitting Your Purple Agent

### Prerequisites

Your purple agent must:
- Support A2A (Agent-to-Agent) protocol
- Handle function calling requests
- Be packaged as a Docker container on GHCR
- Be registered on [agentbeats.dev](https://agentbeats.dev)

### Submission Steps

1. **Fork this repository**

2. **Configure your agent in `scenario.toml`:**
   ```toml
   [[participants]]
   agentbeats_id = "your-purple-agent-id"
   name = "simple_agent"
   env = {
     OPENAI_API_KEY = "${OPENAI_API_KEY}",
     OPENAI_BASE_URL = "${OPENAI_BASE_URL}",
     OPENAI_MODEL = "${OPENAI_MODEL}"
   }

   [config]
   benchmark = "cfb"  # or "bfcl" or "tau2"
   num_tasks = 50     # Number of tasks to evaluate
   ```

3. **Set up GitHub Secrets:**
   - Go to your fork's Settings → Secrets and variables → Actions
   - Add required secrets:
     - `OPENAI_API_KEY`: Your OpenAI API key
     - `OPENAI_BASE_URL`: (Optional) Custom OpenAI endpoint
     - `OPENAI_MODEL`: Model to use (e.g., "gpt-4")
     - `RAPID_API_KEY`: (For CFB) Your RapidAPI key
     - `GHCR_TOKEN`: (Optional) GitHub token for private images

4. **Commit and push `scenario.toml`:**
   ```bash
   git add scenario.toml
   git commit -m "Submit my purple agent"
   git push
   ```

5. **GitHub Actions will automatically:**
   - Pull your purple agent Docker image
   - Run the evaluation
   - Create a submission branch with results
   - Provide a link to create a pull request

6. **Create a pull request** to submit your results to the main leaderboard

## Benchmark Configuration

### Available Benchmarks

- **`bfcl`**: Berkeley Function Calling Leaderboard
  - Test categories: `simple_python`, `multi_turn_base`, `parallel`, `live_simple`, etc.
  - Configurable: `num_tasks`, `test_category`, `sample_ids`

- **`cfb`**: ComplexFuncBench
  - Domains: Car-Rental, Hotel, Restaurant, Attraction, etc.
  - Configurable: `num_tasks`, `sample_ids`

- **`tau2`**: Customer Service Conversations
  - Domains: `airline`, `retail`, `telecom`, `all`
  - Configurable: `num_tasks`, `domain`

### Example Configurations

**Quick BFCL test:**
```toml
[config]
benchmark = "bfcl"
num_tasks = 10
test_category = "simple_python"
```

**Full CFB evaluation:**
```toml
[config]
benchmark = "cfb"
num_tasks = 100
```

**Tau2 multi-domain:**
```toml
[config]
benchmark = "tau2"
domain = "all"
num_tasks = 50
```

## Leaderboard Display

Results are automatically displayed on [agentbeats.dev](https://agentbeats.dev) with:
- Overall performance metrics
- Category/domain breakdowns
- Task-level success rates
- Comparative rankings

## Support & Issues

- Green Agent Repository: [Your GitHub URL]
- AgentBeats Documentation: https://docs.agentbeats.dev
- Issues: Create an issue in this repository

---

**Maintained by:** [Your Name/Organization]
**Green Agent ID:** `019bc5cc-c93e-7372-ad04-ec1115efe810`
