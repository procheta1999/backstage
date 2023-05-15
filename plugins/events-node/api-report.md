## API Report File for "@backstage/plugin-events-node"

> Do not edit this file. It is a report generated by [API Extractor](https://api-extractor.com/).

```ts
// @public
export interface EventBroker {
  publish(params: EventParams): Promise<void>;
  subscribe(
    ...subscribers: Array<EventSubscriber | Array<EventSubscriber>>
  ): void;
}

// @public (undocumented)
export interface EventParams<TPayload = unknown> {
  eventPayload: TPayload;
  metadata?: Record<string, string | string[] | undefined>;
  topic: string;
}

// @public
export interface EventPublisher {
  // (undocumented)
  setEventBroker(eventBroker: EventBroker): Promise<void>;
}

// @public
export abstract class EventRouter implements EventPublisher, EventSubscriber {
  // (undocumented)
  protected abstract determineDestinationTopic(
    params: EventParams,
  ): string | undefined;
  // (undocumented)
  onEvent(params: EventParams): Promise<void>;
  // (undocumented)
  setEventBroker(eventBroker: EventBroker): Promise<void>;
  // (undocumented)
  abstract supportsEventTopics(): string[];
}

// @public
export interface EventSubscriber {
  onEvent(params: EventParams): Promise<void>;
  supportsEventTopics(): string[];
}

// @public (undocumented)
export interface HttpPostIngressOptions {
  // (undocumented)
  topic: string;
  // (undocumented)
  validator?: RequestValidator;
}

// @public (undocumented)
export interface RequestDetails {
  body: unknown;
  headers: Record<string, string | string[] | undefined>;
}

// @public
export interface RequestRejectionDetails {
  // (undocumented)
  payload: unknown;
  // (undocumented)
  status: number;
}

// @public
export interface RequestValidationContext {
  reject(details?: Partial<RequestRejectionDetails>): void;
}

// @public
export type RequestValidator = (
  request: RequestDetails,
  context: RequestValidationContext,
) => Promise<void>;

// @public
export abstract class SubTopicEventRouter extends EventRouter {
  protected constructor(topic: string);
  // (undocumented)
  protected determineDestinationTopic(params: EventParams): string | undefined;
  // (undocumented)
  protected abstract determineSubTopic(params: EventParams): string | undefined;
  // (undocumented)
  supportsEventTopics(): string[];
}
```