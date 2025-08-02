# playwright-api-framework-demo
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Playwright API Testing Framework - Capgemini</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0070ad 0%, #00a3e0 100%);
            color: #333;
            overflow-x: hidden;
        }

        .header {
            background: #fff;
            padding: 20px 0;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            z-index: 1000;
        }

        .header-content {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            align-items: center;
            padding: 0 20px;
        }

        .logo {
            height: 50px;
            margin-right: 30px;
        }

        .title {
            font-size: 28px;
            font-weight: 600;
            color: #0070ad;
        }

        .container {
            max-width: 1200px;
            margin: 100px auto 0;
            padding: 20px;
        }

        .tabs {
            display: flex;
            background: rgba(255,255,255,0.1);
            border-radius: 10px 10px 0 0;
            overflow: hidden;
            margin-bottom: 0;
        }

        .tab {
            flex: 1;
            padding: 15px 20px;
            background: rgba(255,255,255,0.1);
            color: white;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            border: none;
            font-size: 16px;
            font-weight: 500;
        }

        .tab:hover {
            background: rgba(255,255,255,0.2);
        }

        .tab.active {
            background: white;
            color: #0070ad;
            box-shadow: 0 -2px 10px rgba(0,0,0,0.1);
        }

        .slide {
            display: none;
            background: white;
            border-radius: 0 0 10px 10px;
            padding: 40px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            animation: fadeIn 0.5s ease-in-out;
        }

        .slide.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .slide h2 {
            color: #0070ad;
            font-size: 32px;
            margin-bottom: 30px;
            border-bottom: 3px solid #00a3e0;
            padding-bottom: 10px;
        }

        .slide h3 {
            color: #333;
            font-size: 24px;
            margin: 25px 0 15px;
            display: flex;
            align-items: center;
        }

        .slide h3::before {
            content: "▶";
            color: #00a3e0;
            margin-right: 10px;
            font-size: 16px;
        }

        .feature-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }

        .feature-card {
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            padding: 25px;
            border-radius: 10px;
            border-left: 4px solid #00a3e0;
            transition: transform 0.3s ease;
        }

        .feature-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
        }

        .feature-card h4 {
            color: #0070ad;
            font-size: 18px;
            margin-bottom: 10px;
        }

        .code-block {
            background: #2d3748;
            color: #e2e8f0;
            padding: 20px;
            border-radius: 8px;
            margin: 20px 0;
            overflow-x: auto;
            font-family: 'Courier New', monospace;
            position: relative;
        }

        .code-block::before {
            content: "💻 Code Example";
            position: absolute;
            top: -10px;
            left: 20px;
            background: #0070ad;
            color: white;
            padding: 5px 15px;
            border-radius: 15px;
            font-size: 12px;
            font-family: 'Segoe UI', sans-serif;
        }

        .benefits-list {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }

        .benefit-item {
            background: linear-gradient(135deg, #e3f2fd 0%, #bbdefb 100%);
            padding: 20px;
            border-radius: 8px;
            display: flex;
            align-items: center;
        }

        .benefit-item::before {
            content: "✓";
            background: #4caf50;
            color: white;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 15px;
            font-weight: bold;
        }

        .architecture-diagram {
            background: linear-gradient(135deg, #fff3e0 0%, #ffe0b2 100%);
            padding: 30px;
            border-radius: 10px;
            margin: 20px 0;
            text-align: center;
        }

        .footer {
            text-align: center;
            margin-top: 50px;
            padding: 30px;
            background: rgba(255,255,255,0.1);
            border-radius: 10px;
            color: white;
        }

        .footer p {
            font-size: 18px;
            margin-bottom: 10px;
        }

        .footer .capgemini-link {
            color: #ffeb3b;
            text-decoration: none;
            font-weight: bold;
        }

        .stats-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }

        .stat-card {
            background: linear-gradient(135deg, #0070ad 0%, #00a3e0 100%);
            color: white;
            padding: 30px;
            border-radius: 10px;
            text-align: center;
        }

        .stat-number {
            font-size: 36px;
            font-weight: bold;
            margin-bottom: 10px;
        }

        .workflow-steps {
            display: flex;
            justify-content: space-between;
            margin: 30px 0;
            flex-wrap: wrap;
        }

        .step {
            flex: 1;
            min-width: 200px;
            margin: 10px;
            padding: 20px;
            background: linear-gradient(135deg, #e8f5e8 0%, #c8e6c9 100%);
            border-radius: 10px;
            text-align: center;
            position: relative;
        }

        .step::before {
            content: attr(data-step);
            position: absolute;
            top: -15px;
            left: 50%;
            transform: translateX(-50%);
            background: #4caf50;
            color: white;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        @media (max-width: 768px) {
            .tabs {
                flex-direction: column;
            }
            
            .tab {
                border-radius: 0;
            }
            
            .slide {
                padding: 20px;
            }
            
            .title {
                font-size: 20px;
            }
        }
    </style>
</head>
<body>
    <header class="header">
        <div class="header-content">
            <svg class="logo" viewBox="0 0 200 50" xmlns="http://www.w3.org/2000/svg">
                <rect x="0" y="10" width="40" height="30" fill="#0070ad"/>
                <text x="50" y="35" font-family="Arial, sans-serif" font-size="20" font-weight="bold" fill="#0070ad">Capgemini</text>
            </svg>
            <h1 class="title">Playwright API Testing Framework</h1>
        </div>
    </header>

    <div class="container">
        <div class="tabs">
            <button class="tab active" onclick="showSlide(0)">Overview</button>
            <button class="tab" onclick="showSlide(1)">Features</button>
            <button class="tab" onclick="showSlide(2)">Architecture</button>
            <button class="tab" onclick="showSlide(3)">Implementation</button>
            <button class="tab" onclick="showSlide(4)">Best Practices</button>
            <button class="tab" onclick="showSlide(5)">Benefits</button>
        </div>

        <!-- Slide 1: Overview -->
        <div class="slide active">
            <h2>🚀 Playwright API Testing Framework Overview</h2>
            
            <div class="stats-container">
                <div class="stat-card">
                    <div class="stat-number">100%</div>
                    <div>TypeScript Coverage</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">CI/CD</div>
                    <div>Ready Integration</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">Multi</div>
                    <div>Environment Support</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">Advanced</div>
                    <div>Reporting</div>
                </div>
            </div>

            <h3>What is Playwright API Testing?</h3>
            <p>Playwright API testing framework provides a comprehensive solution for automated API testing using TypeScript. It offers robust features for testing REST APIs, handling authentication, data validation, and generating detailed reports.</p>

            <h3>Key Highlights</h3>
            <div class="benefits-list">
                <div class="benefit-item">Cross-platform compatibility</div>
                <div class="benefit-item">Built-in TypeScript support</div>
                <div class="benefit-item">Parallel test execution</div>
                <div class="benefit-item">Comprehensive reporting</div>
                <div class="benefit-item">CI/CD pipeline integration</div>
                <div class="benefit-item">Schema validation support</div>
            </div>
        </div>

        <!-- Slide 2: Features -->
        <div class="slide">
            <h2>✨ Framework Features</h2>
            
            <div class="feature-grid">
                <div class="feature-card">
                    <h4>🔒 Authentication Management</h4>
                    <p>Support for JWT, OAuth, API keys, and custom authentication mechanisms with automatic token refresh.</p>
                </div>
                <div class="feature-card">
                    <h4>🌍 Multi-Environment Support</h4>
                    <p>Easy configuration for dev, staging, and production environments with environment-specific settings.</p>
                </div>
                <div class="feature-card">
                    <h4>📊 Advanced Reporting</h4>
                    <p>HTML, JSON, and JUnit reports with detailed logs, screenshots, and performance metrics.</p>
                </div>
                <div class="feature-card">
                    <h4>🔍 Schema Validation</h4>
                    <p>JSON schema validation for request and response payloads using AJV validator.</p>
                </div>
                <div class="feature-card">
                    <h4>📈 Performance Testing</h4>
                    <p>Built-in performance metrics collection and response time validation.</p>
                </div>
                <div class="feature-card">
                    <h4>🧪 Data-Driven Testing</h4>
                    <p>External JSON files for test data management with parameterized test execution.</p>
                </div>
            </div>

            <div class="code-block">
// Example: API Test with Authentication
import { test, expect } from '@playwright/test';
import { UserService } from '../services/user-service';

test('Create user with authentication', async ({ request }) => {
  const userService = new UserService();
  const userData = { name: 'John Doe', email: 'john@example.com' };
  
  const response = await userService.createUser(request, userData);
  
  expect(response.status()).toBe(201);
  expect(await response.json()).toMatchSchema(userSchema);
});
            </div>
        </div>

        <!-- Slide 3: Architecture -->
        <div class="slide">
            <h2>🏗️ Framework Architecture</h2>
            
            <div class="architecture-diagram">
                <h3>Layered Architecture Approach</h3>
                <div class="workflow-steps">
                    <div class="step" data-step="1">
                        <h4>Test Layer</h4>
                        <p>Test specifications and data-driven test cases</p>
                    </div>
                    <div class="step" data-step="2">
                        <h4>Service Layer</h4>
                        <p>API service classes with business logic abstraction</p>
                    </div>
                    <div class="step" data-step="3">
                        <h4>Helper Layer</h4>
                        <p>Utility functions for authentication, validation, and data generation</p>
                    </div>
                    <div class="step" data-step="4">
                        <h4>Config Layer</h4>
                        <p>Environment configuration and test settings management</p>
                    </div>
                </div>
            </div>

            <h3>Project Structure</h3>
            <div class="code-block">
playwright-api-framework/
├── src/
│   ├── config/          # Environment configurations
│   ├── helpers/         # Utility functions
│   ├── models/          # Data models and interfaces
│   ├── services/        # API service classes
│   └── utils/           # Common utilities
├── tests/
│   ├── api/             # API test specifications
│   ├── data/            # Test data files
│   └── fixtures/        # Test fixtures
├── reports/             # Generated test reports
└── playwright.config.ts # Playwright configuration
            </div>

            <h3>Design Principles</h3>
            <div class="benefits-list">
                <div class="benefit-item">Separation of Concerns</div>
                <div class="benefit-item">Reusable Components</div>
                <div class="benefit-item">Maintainable Code Structure</div>
                <div class="benefit-item">Scalable Architecture</div>
            </div>
        </div>

        <!-- Slide 4: Implementation -->
        <div class="slide">
            <h2>⚡ Implementation Guide</h2>
            
            <h3>Setup and Installation</h3>
            <div class="code-block">
# Clone and setup the framework
git clone <repository-url>
cd playwright-api-framework
npm install
npx playwright install

# Run tests
npm test

# Generate reports
npx playwright show-report
            </div>

            <h3>Service Layer Implementation</h3>
            <div class="code-block">
// UserService Example
export class UserService {
  private baseURL: string;

  constructor() {
    this.baseURL = config.baseURL;
  }

  async createUser(request: APIRequestContext, userData: any) {
    return await request.post(`${this.baseURL}/users`, {
      data: userData,
      headers: { 'Authorization': `Bearer ${config.apiToken}` }
    });
  }

  async getUserById(request: APIRequestContext, userId: string) {
    return await request.get(`${this.baseURL}/users/${userId}`);
  }
}
            </div>

            <h3>Test Implementation</h3>
            <div class="code-block">
// API Test Example
test.describe('User Management API', () => {
  test('Should create and retrieve user', async ({ request }) => {
    const userService = new UserService();
    const userData = generateUserData();

    // Create user
    const createResponse = await userService.createUser(request, userData);
    expect(createResponse.status()).toBe(201);

    // Retrieve user
    const userId = (await createResponse.json()).id;
    const getResponse = await userService.getUserById(request, userId);
    expect(getResponse.status()).toBe(200);
  });
});
            </div>
        </div>

        <!-- Slide 5: Best Practices -->
        <div class="slide">
            <h2>📋 Best Practices & Guidelines</h2>
            
            <h3>Testing Best Practices</h3>
            <div class="feature-grid">
                <div class="feature-card">
                    <h4>🎯 Test Organization</h4>
                    <p>Group related tests, use descriptive names, and maintain clear test hierarchies.</p>
                </div>
                <div class="feature-card">
                    <h4>🔄 Data Management</h4>
                    <p>Use external JSON files, implement data factories, and ensure test data isolation.</p>
                </div>
                <div class="feature-card">
                    <h4>🛡️ Error Handling</h4>
                    <p>Implement comprehensive error handling, logging, and graceful failure management.</p>
                </div>
                <div class="feature-card">
                    <h4>⚡ Performance</h4>
                    <p>Optimize parallel execution, minimize dependencies, and implement efficient retry mechanisms.</p>
                </div>
            </div>

            <h3>Code Quality Guidelines</h3>
            <div class="code-block">
// Example: Proper error handling and validation
test('API error handling example', async ({ request }) => {
  try {
    const response = await userService.createUser(request, invalidData);
    
    // Validate error response
    expect(response.status()).toBe(400);
    
    const errorBody = await response.json();
    expect(errorBody).toHaveProperty('error');
    expect(errorBody.error).toContain('validation failed');
    
  } catch (error) {
    logger.error(`Test failed: ${error.message}`);
    throw error;
  }
});
            </div>

            <h3>CI/CD Integration</h3>
            <div class="benefits-list">
                <div class="benefit-item">GitHub Actions workflow setup</div>
                <div class="benefit-item">Environment-specific test execution</div>
                <div class="benefit-item">Automated report generation</div>
                <div class="benefit-item">Slack/Teams notifications</div>
                <div class="benefit-item">Test result artifacts</div>
                <div class="benefit-item">Performance trend monitoring</div>
            </div>
        </div>

        <!-- Slide 6: Benefits -->
        <div class="slide">
            <h2>🎯 Business Benefits & ROI</h2>
            
            <div class="stats-container">
                <div class="stat-card">
                    <div class="stat-number">60%</div>
                    <div>Faster Test Development</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">90%</div>
                    <div>Test Coverage Improvement</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">40%</div>
                    <div>Reduced Maintenance Cost</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">24/7</div>
                    <div>Continuous Testing</div>
                </div>
            </div>

            <h3>Technical Benefits</h3>
            <div class="feature-grid">
                <div class="feature-card">
                    <h4>🚀 Rapid Development</h4>
                    <p>Accelerated test automation development with reusable components and standardized patterns.</p>
                </div>
                <div class="feature-card">
                    <h4>🔒 Reliability</h4>
                    <p>Consistent test execution with built-in retry mechanisms and error handling.</p>
                </div>
                <div class="feature-card">
                    <h4>📈 Scalability</h4>
                    <p>Easily scalable framework supporting multiple projects and environments.</p>
                </div>
                <div class="feature-card">
                    <h4>🔍 Visibility</h4>
                    <p>Comprehensive reporting and metrics for informed decision-making.</p>
                </div>
            </div>

            <h3>Business Impact</h3>
            <div class="benefits-list">
                <div class="benefit-item">Reduced time-to-market</div>
                <div class="benefit-item">Improved software quality</div>
                <div class="benefit-item">Lower operational costs</div>
                <div class="benefit-item">Enhanced team productivity</div>
                <div class="benefit-item">Better risk management</div>
                <div class="benefit-item">Increased customer satisfaction</div>
            </div>

            <div class="architecture-diagram">
                <h3>🎉 Ready to Get Started?</h3>
                <p style="font-size: 18px; margin: 20px 0;">
                    Transform your API testing strategy with Playwright Framework
                </p>
                <div style="margin-top: 30px;">
                    <strong>Next Steps:</strong>
                    <ol style="text-align: left; display: inline-block; margin-top: 15px;">
                        <li>Review the framework documentation</li>
                        <li>Set up your first test project</li>
                        <li>Integrate with your CI/CD pipeline</li>
                        <li>Start automating your API tests</li>
                    </ol>
                </div>
            </div>
        </div>
    </div>

    <footer class="footer">
        <p>Playwright API Testing Framework</p>
        <p>Powered by <a href="#" class="capgemini-link">Capgemini Engineering</a></p>
        <p style="font-size: 14px; margin-top: 15px;">© 2025 Capgemini. All rights reserved.</p>
    </footer>

    <script>
        function showSlide(index) {
            // Hide all slides
            const slides = document.querySelectorAll('.slide');
            const tabs = document.querySelectorAll('.tab');
            
            slides.forEach(slide => slide.classList.remove('active'));
            tabs.forEach(tab => tab.classList.remove('active'));
            
            // Show selected slide and tab
            slides[index].classList.add('active');
            tabs[index].classList.add('active');
        }

        // Add keyboard navigation
        document.addEventListener('keydown', (e) => {
            const activeTab = document.querySelector('.tab.active');
            const tabs = document.querySelectorAll('.tab');
            const currentIndex = Array.from(tabs).indexOf(activeTab);
            
            if (e.key === 'ArrowRight' && currentIndex < tabs.length - 1) {
                showSlide(currentIndex + 1);
            } else if (e.key === 'ArrowLeft' && currentIndex > 0) {
                showSlide(currentIndex - 1);
            }
        });

        // Add smooth scrolling for better UX
        document.querySelectorAll('.tab').forEach(tab => {
            tab.addEventListener('click', () => {
                window.scrollTo({ top: 0, behavior: 'smooth' });
            });
        });
    </script>
</body>
</html>
