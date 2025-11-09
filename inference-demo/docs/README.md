# Inference Demo Documentation

## Overview

The Inference Demo is a web-based interface for testing LLM inference on Hypernode's distributed GPU network. It provides real-time metrics, cost comparisons, and performance benchmarks.

## Features

### 1. Model Testing Interface
- Select from available models deployed on Hypernode
- Input custom prompts
- Receive inference results with latency metrics
- Compare token generation speed

### 2. Performance Metrics
- **Latency**: Time to first token (TTFT) and total inference time
- **Throughput**: Tokens per second
- **Cost**: Real-time cost-per-token calculation
- **Comparison**: Side-by-side with centralized providers

### 3. SDK Examples
- JavaScript/TypeScript integration examples
- Python SDK usage patterns
- REST API direct integration

## Architecture

```
inference-demo/frontend/
├── src/
│   ├── pages/
│   │   ├── InferenceDemo.jsx    # Main testing interface
│   │   ├── Benchmarks.jsx       # Performance comparisons
│   │   └── Comparison.jsx       # Provider comparison
│   ├── components/
│   │   ├── ModelSelector.jsx    # Model selection UI
│   │   ├── PromptInput.jsx      # Prompt entry component
│   │   ├── ResultsDisplay.jsx   # Inference results
│   │   └── MetricsPanel.jsx     # Live metrics dashboard
│   └── lib/
│       ├── api.js               # Hypernode API client
│       └── metrics.js           # Metrics calculation
```

## API Integration

### Hypernode Backend API

The demo connects to Hypernode's backend API to submit inference jobs and retrieve results.

**Endpoint**: `POST /api/jobs/inference`

**Request**:
```json
{
  "model": "llama-2-7b",
  "prompt": "Explain quantum computing",
  "max_tokens": 512,
  "temperature": 0.7
}
```

**Response**:
```json
{
  "job_id": "j_abc123",
  "status": "processing",
  "estimated_time": 15000
}
```

### Job Status Polling

**Endpoint**: `GET /api/jobs/{job_id}`

**Response**:
```json
{
  "job_id": "j_abc123",
  "status": "completed",
  "result": {
    "text": "Quantum computing leverages...",
    "tokens_generated": 127,
    "latency_ms": 4230,
    "ttft_ms": 320,
    "cost_sol": 0.00042
  },
  "metrics": {
    "node_id": "node_xyz789",
    "gpu_model": "RTX 4090",
    "tokens_per_second": 30.02
  }
}
```

## Configuration

### Environment Variables

Create `.env` in `inference-demo/frontend/`:

```env
VITE_HYPERNODE_API=https://api.hypernode.network
VITE_SOLANA_RPC=https://api.devnet.solana.com
VITE_REFRESH_INTERVAL=2000
```

### Model Configuration

Available models are fetched from the API endpoint:

**Endpoint**: `GET /api/models/available`

**Response**:
```json
{
  "models": [
    {
      "id": "llama-2-7b",
      "name": "Llama 2 7B",
      "context_length": 4096,
      "cost_per_token": 0.0000033
    },
    {
      "id": "mistral-7b",
      "name": "Mistral 7B Instruct",
      "context_length": 8192,
      "cost_per_token": 0.0000035
    }
  ]
}
```

## Development

### Prerequisites

- Node.js 18+
- npm or yarn
- Access to Hypernode Backend API

### Setup

```bash
cd inference-demo/frontend
npm install
cp .env.example .env
# Edit .env with your configuration
npm run dev
```

### Build for Production

```bash
npm run build
# Output in dist/
```

## Usage Examples

### JavaScript SDK Integration

```javascript
import { HypernodeClient } from '@hypernode/sdk';

const client = new HypernodeClient({
  apiUrl: 'https://api.hypernode.network',
  apiKey: 'your_api_key'
});

const result = await client.inference({
  model: 'llama-2-7b',
  prompt: 'Write a haiku about distributed computing',
  maxTokens: 50
});

console.log(result.text);
console.log(`Cost: ${result.cost_sol} SOL`);
console.log(`Latency: ${result.latency_ms}ms`);
```

### Python SDK Integration

```python
from hypernode import Client

client = Client(
    api_url="https://api.hypernode.network",
    api_key="your_api_key"
)

result = client.inference(
    model="mistral-7b",
    prompt="Explain blockchain in simple terms",
    max_tokens=100
)

print(result.text)
print(f"Cost: {result.cost_sol} SOL")
print(f"Tokens/sec: {result.tokens_per_second}")
```

### Direct REST API

```bash
curl -X POST https://api.hypernode.network/api/jobs/inference \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "llama-2-7b",
    "prompt": "Write a poem about GPUs",
    "max_tokens": 128
  }'
```

## Metrics Explanation

### Latency Metrics

- **TTFT (Time To First Token)**: Measures prompt processing + first token generation
- **Total Latency**: Complete inference time from submission to final token
- **Network Latency**: Time spent in network transmission (excluded from compute metrics)

### Cost Calculation

```
Total Cost (SOL) = tokens_generated × cost_per_token + base_fee
```

Where:
- `base_fee`: Fixed cost per job (covers Solana transaction fees)
- `cost_per_token`: Variable cost based on model and GPU type

### Throughput

```
Tokens per second = tokens_generated / (latency_ms / 1000)
```

## Comparison with Centralized Providers

The demo includes benchmarks against:
- OpenAI API (GPT-3.5/GPT-4)
- Anthropic Claude
- Google PaLM
- Cohere

**Comparison metrics:**
- Cost per 1M tokens
- Average latency for 100-token generation
- Throughput (tokens/sec)
- Geographic availability

## Roadmap

- [ ] Real-time streaming responses (SSE)
- [ ] Batch inference support
- [ ] Custom model deployment interface
- [ ] Advanced metrics dashboard (GPU utilization, queue depth)
- [ ] Historical performance charts

## Support

For issues or questions:
- GitHub Issues: https://github.com/Hypernode-sol/Virtual-Agent/issues
- Email: contact@hypernodesolana.org
- Documentation: https://docs.hypernode.network

---

**Note**: This is a demonstration interface. For production use, integrate directly with Hypernode's official SDK or REST API.
